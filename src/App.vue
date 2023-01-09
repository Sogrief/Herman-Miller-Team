import { RouterView } from 'vue-router'
import axios from 'axios'

<template>
  <RouterView />
</template>

}
const response = await axios.get(url 'http://localhost/herman/wp-json/wp/v2')
if (response.status === 200) {
  console.log(response.data)
}