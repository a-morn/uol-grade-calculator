<template>
    {{ level }} | {{ code }} | {{ compulsory }} | {{ credits }}
</template>

<script>
export default {
  name: 'Class',
  props: {
    level: {
        type: Number,
        required: true
    },
    code: {
        type: String,
        required: true
    },
    compulsory: {
        type: Boolean,
        required: true
    },
    credits: {
        type: Number,
        required: true
    }
  }
}
</script>