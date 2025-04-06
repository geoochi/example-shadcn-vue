<script setup lang="ts">
import { cn } from '@/lib/utils'
import { Button } from '@/components/ui/button'
import { FormControl, FormDescription, FormField, FormItem, FormLabel, FormMessage } from '@/components/ui/form'
import { Popover, PopoverContent, PopoverTrigger } from '@/components/ui/popover'
import { toast } from 'vue-sonner'
import { DateFormatter, getLocalTimeZone, parseDate, today } from '@internationalized/date'
import { toTypedSchema } from '@vee-validate/zod'
import { CalendarIcon } from 'lucide-vue-next'
import { toDate, createYear, createDecade } from 'reka-ui/date'
import { useForm } from 'vee-validate'
import { computed, type HTMLAttributes, type Ref } from 'vue'
import { z } from 'zod'
import { useVModel } from '@vueuse/core'
import { type DateValue } from 'reka-ui/date'
import { CalendarRoot, CalendarRootEmits, CalendarRootProps, useDateFormatter, useForwardPropsEmits } from 'reka-ui'

const props = withDefaults(defineProps<CalendarRootProps & { class?: HTMLAttributes['class'] }>(), {
  modelValue: undefined,
  placeholder() {
    return today(getLocalTimeZone())
  },
  weekdayFormat: 'short',
})
const emits = defineEmits<CalendarRootEmits>()

const delegatedProps = computed(() => {
  const { class: _, placeholder: __, ...delegated } = props

  return delegated
})

const placeholder = useVModel(props, 'modelValue', emits, {
  passive: true,
  defaultValue: today(getLocalTimeZone()),
}) as Ref<DateValue>

const forwarded = useForwardPropsEmits(delegatedProps, emits)

const formatter = useDateFormatter('en')

const df = new DateFormatter('en-US', {
  dateStyle: 'long',
})

const formSchema = toTypedSchema(
  z.object({
    dob: z.string().refine(v => v, { message: 'A date of birth is required.' }),
  })
)

const { handleSubmit, setFieldValue, values } = useForm({
  validationSchema: formSchema,
})

const value = computed({
  get: () => (values.dob ? parseDate(values.dob) : undefined),
  set: val => val,
})

const onSubmit = handleSubmit(values => {
  toast('You submitted the following values:', { description: values.dob })
})
</script>

<template>
  <form class="space-y-8" @submit="onSubmit">
    <FormField name="dob">
      <FormItem class="flex flex-col">
        <FormLabel>Date of birth</FormLabel>
        <Popover>
          <PopoverTrigger as-child>
            <FormControl>
              <Button
                variant="outline"
                :class="cn('w-[240px] ps-3 text-start font-normal', !value && 'text-muted-foreground')"
              >
                <span>{{ value ? df.format(toDate(value)) : 'Pick a date' }}</span>
                <CalendarIcon class="ms-auto h-4 w-4 opacity-50" />
              </Button>
              <input hidden />
            </FormControl>
          </PopoverTrigger>
          <PopoverContent class="w-auto p-0">
            <CalendarRoot
              v-slot="{ date, grid, weekDays }"
              v-model:placeholder="placeholder"
              v-model="value"
              @update:model-value="
                (v: DateValue) => {
                  if (v) {
                    setFieldValue('dob', v.toString())
                  } else {
                    setFieldValue('dob', undefined)
                  }
                }
              "
              v-bind="forwarded"
              :class="cn('rounded-md border p-3', props.class)"
            >
              <CalendarHeader>
                <CalendarHeading class="flex w-full items-center justify-between gap-2">
                  <Select
                    :default-value="placeholder.month.toString()"
                    @update:model-value="
                        (v: string) => {
                        if (!v || !placeholder) return
                        if (Number(v) === placeholder?.month) return
                        placeholder = placeholder.set({
                            month: Number(v),
                        })
                        }
                    "
                  >
                    <SelectTrigger aria-label="Select month" class="w-[60%]">
                      <SelectValue placeholder="Select month" />
                    </SelectTrigger>
                    <SelectContent class="max-h-[200px]">
                      <SelectItem
                        v-for="month in createYear({ dateObj: date })"
                        :key="month.toString()"
                        :value="month.month.toString()"
                      >
                        {{ formatter.custom(toDate(month), { month: 'long' }) }}
                      </SelectItem>
                    </SelectContent>
                  </Select>

                  <Select
                    :default-value="placeholder.year.toString()"
                    @update:model-value="
                        (v: string) => {
                        if (!v || !placeholder) return
                        if (Number(v) === placeholder?.year) return
                        placeholder = placeholder.set({
                            year: Number(v),
                        })
                        }
                    "
                  >
                    <SelectTrigger aria-label="Select year" class="w-[40%]">
                      <SelectValue placeholder="Select year" />
                    </SelectTrigger>
                    <SelectContent class="max-h-[200px]">
                      <SelectItem
                        v-for="yearValue in createDecade({ dateObj: date, startIndex: -10, endIndex: 10 })"
                        :key="yearValue.toString()"
                        :value="yearValue.year.toString()"
                      >
                        {{ yearValue.year }}
                      </SelectItem>
                    </SelectContent>
                  </Select>
                </CalendarHeading>
              </CalendarHeader>

              <div class="flex flex-col space-y-4 pt-4 sm:flex-row sm:gap-x-4 sm:gap-y-0">
                <CalendarGrid v-for="month in grid" :key="month.value.toString()">
                  <CalendarGridHead>
                    <CalendarGridRow>
                      <CalendarHeadCell v-for="day in weekDays" :key="day">
                        {{ day }}
                      </CalendarHeadCell>
                    </CalendarGridRow>
                  </CalendarGridHead>
                  <CalendarGridBody class="grid">
                    <CalendarGridRow
                      v-for="(weekDates, index) in month.rows"
                      :key="`weekDate-${index}`"
                      class="mt-2 w-full"
                    >
                      <CalendarCell v-for="weekDate in weekDates" :key="weekDate.toString()" :date="weekDate">
                        <CalendarCellTrigger :day="weekDate" :month="month.value" />
                      </CalendarCell>
                    </CalendarGridRow>
                  </CalendarGridBody>
                </CalendarGrid>
              </div>
            </CalendarRoot>
          </PopoverContent>
        </Popover>
        <FormDescription> Your date of birth is used to calculate your age. </FormDescription>
        <FormMessage />
      </FormItem>
    </FormField>
    <Button type="submit"> Submit </Button>
  </form>
</template>
