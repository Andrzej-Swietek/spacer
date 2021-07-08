<template>
  <div class="searchWrapper">
<!--    <label for="search">Search</label>-->
    <input
      id="search"
      name="search"
      type="text"
      :value="value"
      :class="{ dark: dark }"
      @input="handleChange"
    />
  </div>

</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
  .searchWrapper {
    display: flex;
    flex-direction: column;
    width: 250px;
    margin-top: 50px;

    label {
      font-family: Montserrat, sans-serif;
    }

    input {
      height: 30px;
      border: 0;
      border-bottom: 1px solid white;
      background: none;
      transition: box-shadow 0.3s ease-out;
      color: white;
      text-align: center;
      font-size: 18px;
      font-weight: 300;
      @media (min-width: 1024px) {
        font-weight: 400;
      }

      &:focus {
        outline: none;
        box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.3);
      }
    }

    input.dark {
      color: #1E3D4A;
      border-bottom-color: #1E3D4A;

      &:focus {
        outline: none;
        box-shadow: 0 10px 20px -8px rgba(30, 61, 74, 0.2);
      }
    }
  }
</style>
