<template>
  <div>
      <table class="table">
        <thead>
          <tr>
            <th>Office Transaction</th>
            <th @click="handlePopup">+ Add Transaction</th>
          </tr>
          <tr>
            <th> Date </th>
            <th> Description </th>
            <th> Credit </th>
            <th> Debit </th>
            <th> Running Balance </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in initialData" :key="index">
            <td> {{item.date}} </td>
            <td> {{item.description}} </td>
            <td> {{item.credit}} </td>
            <td> {{item.debit}} </td>
            <td> {{item.running_bal}} </td>
          </tr>
        </tbody>
      </table>
      <div v-if="showTransationPopup">
        <div>
            <label> Transaction Type</label>
            <select v-model="transactionType">
                <option value="credit">Credit</option>
                <option value="debit">Debit</option>
            </select>
        </div>                  
        <div>
          <label>Amount</label>
          <input type="text" class="border" v-model="amount">
        </div>
        <div>
          <label>Description</label>
          <textarea rows="4" cols="30" v-model="description" class="border"></textarea>
        </div>
        <button @click="handleSave">Save</button>
        <button @click="canclePopop">Cancel</button>
      </div>
  </div>
</template>

<script>
export default {
  name: 'App',

  components: {
  },
  data(){
    return {
      initialData: [
        {
          'date': '18/09/2020',
          'description': 'Credit to Office Account',
          'credit': 5000,
          'debit': '',
          'running_bal': 5000
        }
      ],
      showTransationPopup: false,
      amount: '',
      description: '',
      transactionType: ''
    }
  },
  methods: {
    handleSave() {
      let data = {}
      if(this.transactionType === 'credit') {
        data.running_bal = parseFloat(this.initialData[0].running_bal) + parseFloat(this.amount)
        data.credit = this.amount
        data.debit = ''
      } else {
        data.running_bal = parseFloat(this.initialData[0].running_bal) - parseFloat(this.amount)
        data.credit = ''
        data.debit = this.amount
      }
      data.date = new Date()
      data.description = this.description
      this.initialData.unshift(data)
    },
    handlePopup(){
      this.showTransationPopup = true
    },
    canclePopop() {
      this.amount = ''
      this.description = ''
      this.transactionType = ''
      this.showTransationPopup = false
    }
  }
}
</script>

<style>

</style>
