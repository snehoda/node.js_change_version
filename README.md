const axios = require('axios')
require('dotenv/config');

(async () => {
  const config = {
    baseURL: process.env.BASE_URL,
    validateStatus: () => true
  }

  let response = await axios({
    method: 'POST',
    url: '/auth',
    data: {
      login: process.env.LOGIN,
      password: process.env.PASSWORD,
    },
    ...config
    })
  
  const token = response.data.token

  response = await axios({
    method: 'POST',
    url: '/users',
    headers: {
      Authorization: token
    },
    ...config
    })
  
  console.log(`User 1: ${response.data.id}`)

  response = await axios({
    method: 'POST',
    url: '/users',
    headers: {
      Authorization: token
    },
    ...config
    })
  
  console.log(`User 2: ${response.data.id}`)
})()
