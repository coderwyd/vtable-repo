<template>
  <div>
    <div
      style="
        margin-bottom: 16px;
        display: flex;
        align-items: center;
        justify-content: space-between;
      "
    >
      <div>
        <a-tag color="blue">总数据: {{ totalCount }} 条</a-tag>
        <a-tag color="green">当前页: {{ pagination.pageIndex }}</a-tag>
      </div>
      <a-radio-group v-model:value="paginationPlacement" button-style="solid">
        <a-radio-button value="left">左对齐</a-radio-button>
        <a-radio-button value="center">居中</a-radio-button>
        <a-radio-button value="right">右对齐</a-radio-button>
      </a-radio-group>
    </div>

    <VTable
      v-model:default-pagination="pagination"
      :data="tableData"
      :columns="columns"
      :loading="loading"
      :pagination-config="{
        enabled: true,
        placement: paginationPlacement,
        total: totalCount,
        mode: 'client',
      }"
    />
  </div>
</template>

<script setup lang="ts">
import VTable, {
  type VTableColumn,
  type VTablePaginationState,
} from "@aimerthyr/virtual-table";
import { ref } from "vue";

defineOptions({ name: "PaginationExample" });

const loading = ref(false);
const totalCount = ref(200);
const paginationPlacement = ref<"left" | "center" | "right">("right");

const pagination = ref<VTablePaginationState>({
  pageIndex: 1,
  pageSize: 10,
});

const id = 1;
const tableData = ref<any[]>([
  {
    id,
    name: `员工${id}`,
    age: 20 + (id % 30),
    email: `user${id}@example.com`,
    department: ["技术部", "产品部", "运营部", "市场部"][id % 4],
    position: ["工程师", "经理", "专员", "主管"][id % 4],
  },
]);

const columns: VTableColumn[] = [
  { columnKey: "id", columnHeader: "ID", columnWidth: 80 },
  { columnKey: "name", columnHeader: "姓名", columnWidth: 120 },
  {
    columnKey: "age",
    columnHeader: "年龄",
    columnWidth: 100,
    columnAlign: "center",
  },
  { columnKey: "email", columnHeader: "邮箱", columnWidth: 200 },
  { columnKey: "department", columnHeader: "部门", columnWidth: 120 },
  { columnKey: "position", columnHeader: "职位" },
];
</script>
