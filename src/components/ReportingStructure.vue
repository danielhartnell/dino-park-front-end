<template>
  <div class="reporting-structure">
    <div class="reporting-structure__reports-to">
      <slot name="reports-to"></slot>
    </div>
    <div class="reporting-structure__manages">
      <slot name="manages"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ReportingStructure',
};
</script>

<style>
  .reporting-structure {
    display: flex;
    flex-direction: column;
  }
  @media(min-width:50em){
    .reporting-structure {
      flex-direction: row;
    }
  }
    .reporting-structure__reports-to {
      flex: 1;
      background-color: var(--gray-10);
      border-right: 1px solid var(--gray-20);
    }
    .reporting-structure__manages {
      padding: 1.5em;
      flex: 2;
    }

  /* @TODO make more elegant  */
  .profile__section .reporting-structure {
    margin: -1.5em -1.5em -1.5em -1.5em;
  }

  .profile__section .reporting-structure > div {
    padding: 1.5em 1.5em 5em;
  }
</style>
