<template>
    <div class="
      foo
      d-ba
      d-m16
      d-p32
      d-py128
      d-baw4
      d-bas-dashed
      d-bar16
    ">
      <div class="d-headline--xl">
        Wizbang animatey playbook items go here.
      </div>
    </div>
  </template>
  <style lang="less" scoped>
    .foo {
      background-color: var(--dt-color-surface-secondary);
      color: var(--dt-color-foreground-tertiary);
      animation: wizbang 1s infinite ease-in-out alternate;
    }
  
    @keyframes wizbang {
      to {
        color: var(--dt-color-foreground-success);
        background-color: var(--dt-color-surface-primary);
      }
    }
  </style>
  