<script setup>
import chartInfo from '@images/cards/chart-info.png'

const transactions = [
  {
    amount: +1,
    paymentMethod: 'Lot 1',
    description: 'Space 2D',
    color: 'error',
  },
  {
    paymentMethod: 'Lot 5',
    amount: +1,
    description: 'Space 4A',
    color: 'primary',
  },
  {
    amount: +1,
    paymentMethod: 'Lot 2',
    description: 'Space 7F',
    color: 'info',
  },
  {
    paymentMethod: 'Lot 3',
    amount: -1,
    description: 'Space 6B',
    color: 'success',
  },
  {
    paymentMethod: 'Lot 5',
    amount: -1,
    description: 'Space 3C',
    color: 'primary',
  },
]

const moreList = [
  {
    title: 'Share',
    value: 'Share',
  },
  {
    title: 'Refresh',
    value: 'Refresh',
  },
  {
    title: 'Update',
    value: 'Update',
  },
]
</script>

<template>
  <VCard title="Parking Lot Availability">
    <template #append>
      <div class="me-n3 mt-n2">
        <MoreBtn :menu-list="moreList" />
      </div>
    </template>

    <VCardText>
      <VList class="card-list">
        <VListItem
          v-for="item in transactions"
          :key="item.paymentMethod"
        >
          <template #prepend>
            <VAvatar
              rounded
              variant="tonal"
              :color="item.color"
              :image="item.icon"
              class="me-3"
            />
          </template>

          <VListItemSubtitle class="text-disabled mb-1">
            {{ item.paymentMethod }}
          </VListItemSubtitle>
          <VListItemTitle>
            {{ item.description }}
          </VListItemTitle>

          <template #append>
            <VListItemAction>
              <span class="me-1">{{ item.amount > 0 ? `+${Math.abs(item.amount)}` : `-${Math.abs(item.amount)}` }}</span>
            </VListItemAction>
          </template>

        </VListItem>
      </VList>
    </VCardText>
  </VCard>
</template>

<style lang="scss" scoped>
  .card-list {
    --v-card-list-gap: 1.6rem;
  }
</style>
