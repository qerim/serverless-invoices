<template>
    <div>
        <h3>{{ $t('invoice_title') }}</h3>
        {{ $t('issued_at') }}
        <span class="editable__item" v-b-modal.modal_issued_at>{{ invoice.issued_at | date('D MMM YYYY', 'YYYY-MM-DD') }}</span>
        <BModal id="modal_issued_at"
                centered
                :title="$t('modal_issued_at_title')"
                hide-footer
                size="sm"
                content-class="bg-base dp--24">
            <AppDatePicker :value="invoice.issued_at"
                           @change="updateProp({ issued_at: $event })"
                           :errors="errors"
                           :inline="true"
                           field="issued_at"/>
        </BModal>
    </div>
</template>
<script>
import { BModal, VBModal } from 'bootstrap-vue';
import AppEditable from '@/components/form/AppEditable';
import AppDatePicker from '@/components/form/AppDatePicker';
import { formatDate } from '@/filters/date.filter';
import { formatCurrency } from '@/filters/currency.filter';

export default {
  i18nOptions: { namespaces: 'invoice-header' },
  props: ['invoice', 'errors'],
  components: {
    AppEditable,
    AppDatePicker,
    BModal,
  },
  directives: {
    'b-modal': VBModal,
  },
  filters: {
    date: formatDate,
    currency: formatCurrency,
  },
  methods: {
    updateProp(props) {
      this.$emit('update', props);
    },
  },
};
</script>
