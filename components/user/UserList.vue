<template>
  <n-space vertical :size="12">
    <n-data-table
        :bordered="false"
        :single-line="false"
        :columns="columns"
        :data="userList"
        :pagination="pagination"
    />
  </n-space>
</template>

<script setup lang="ts">
import { DataTableColumn, NButton, NTag} from "naive-ui";

const columns =
    [
      {
        title: 'Name',
        key: 'name'
      },
      {
        title: 'Age',
        key: 'age'
      },
      {
        title: 'Address',
        key: 'address'
      },
      {
        title: 'Tags',
        key: 'tags',
        render (row:any) {
          const tags = row.tags.map((tagKey) => {
            return h(
                NTag,
                {
                  style: {
                    marginRight: '6px'
                  },
                  type: 'info',
                  bordered: false
                },
                {
                  default: () => tagKey
                }
            )
          })
          return tags
        }
      },
      {
        title: 'Action',
        key: 'actions',
        render (row:any) {
          return h(
              NButton,
              {
                size: 'small',
                onClick: () => alert(row)
              },
              { default: () => 'Send Email' }
          )
        }
      }
    ]
const pagination = {
  pageSize: 10
}
//TODO user 가데이터 -> 입력데이터로 변환필요
const { data: userList } = await useFetch('/api/userList');
</script>

<style scoped>

</style>
