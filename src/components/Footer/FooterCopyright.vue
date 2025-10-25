<template>
  <div class="footer-copy">
    <p>© {{ new Date().getFullYear() }} RELOAD</p> PRIVACY POLICY. TERMS & CONDITION.
  </div>
</template>

<style scoped lang="scss">
.footer-copy {
  width: 92%;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-between;
  text-align: center;
  font-size: 0.85rem;
  color: #64748b;
  padding-top: 1rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}
</style>
