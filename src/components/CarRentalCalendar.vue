<template>
    <div class="container my-4">
        <div class="row">
            <div class="col-md"></div>
            <div class="col-md-4">
                <div class="form-group">
                    <label for="fromdate">Book From:</label>
                    <input id="fromdate" type="date" class="form-control" v-model="fromDate"
                           @change="updateToDate(); updateDate(fromDate, toDate)" :min="minDate" />
                </div>
            </div>
            <div class="col-md-4">
                <div class="form-group">
                    <label for="todate">To:</label>
                    <input id="todate" type="date" class="form-control" v-model="toDate"
                           @change="updateDate(fromDate, toDate)" :min="fromDate" />
                </div>
            </div>
            <div class="col-md"></div>
        </div>
    </div>
  </template>
<script>
export default {
    data() {
        return {
            fromDate: '',
            toDate: '',
            minDate: this.formatDate(new Date()),
        };
    },
    methods: {
        formatDate(date) {
            return date.toISOString().split('T')[0];
        },
        updateToDate() {
            if (this.toDate && this.toDate < this.fromDate) {
                this.toDate = this.fromDate;
            }
        },
        updateDate(fromDate, toDate) {
            const from = fromDate ? new Date(fromDate) : null;
            const to = toDate ? new Date(toDate) : null;
            if (from && to) {
                const fromYearMonthDay = { year: from.getFullYear(), month: from.getMonth() + 1, day: from.getDate() };
                const toYearMonthDay = { year: to.getFullYear(), month: to.getMonth() + 1, day: to.getDate() };
                this.$emit('update-dates', { fromYearMonthDay, toYearMonthDay });
            }
        }
    },
};
</script>
  
<style>
</style>
