<template>
  <div class="table-scroll">
    <table class="order-table">
      <thead><tr><th>주문번호</th><th>주문자</th><th>상품</th><th>결제금액</th><th>주문상태</th><th>주문일시</th><th /></tr></thead>
      <tbody><tr v-for="order in orders" :key="order.id"><td><button class="order-id">#{{ order.id }}</button></td><td><strong>{{ order.name }}</strong></td><td><p>{{ order.product }}<small v-if="order.items>1"> 외 {{ order.items-1 }}건</small></p></td><td class="amount">₩{{ order.total.toLocaleString() }}</td><td><select :value="order.status" :class="statusClass(order.status)" @change="$emit('change-status',{order,status:$event.target.value})"><option v-for="status in statuses" :key="status">{{ status }}</option></select></td><td>{{ order.time }}</td><td><button class="arrow">›</button></td></tr></tbody>
    </table>
  </div>
</template>
<script setup>
defineProps({orders:{type:Array,required:true}})
defineEmits(['change-status'])
const statuses=['결제완료','배송준비','배송중','배송완료','취소요청']
function statusClass(s){return s==='결제완료'?'paid':s==='배송준비'?'ready':s==='배송중'?'shipping':s==='배송완료'?'done':'cancel'}
</script>
<style scoped>
.table-scroll{overflow:auto}.order-table{width:100%;border-collapse:collapse;min-width:760px}.order-table th{background:#fafafa;color:#8b8e94;font-size:8px;text-align:left;font-weight:600;padding:11px 15px;border-top:1px solid #eee;border-bottom:1px solid #e7e8ea}.order-table td{padding:13px 15px;border-bottom:1px solid #efeff0;font-size:9px;color:#666}.order-table tbody tr:hover{background:#fbfbfb}.order-id{border:0;background:none;color:#31343a;font:9px 'DM Sans';font-weight:600}.order-table td strong{font-size:10px;color:#333}.order-table td p{max-width:190px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}.order-table td small{color:#999}.amount{font-weight:600;font-variant-numeric:tabular-nums;color:#333!important}.order-table select{border:0;border-radius:12px;padding:5px 8px;font:8px 'DM Sans';outline:0}.order-table select.paid{background:#e9f1fb;color:#426f9f}.order-table select.ready{background:#fff0e5;color:#b86d32}.order-table select.shipping{background:#eeeafb;color:#6e57a3}.order-table select.done{background:#e8f4ec;color:#397c4c}.order-table select.cancel{background:#fae9e8;color:#bd514b}.arrow{border:0;background:none;color:#aaa;font-size:17px}
</style>
