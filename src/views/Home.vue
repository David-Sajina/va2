<template>	
	<v-container style="margin-top:10px; margin-bottom:10px;">
		<v-layout row wrap style><!-- 
       <v-text-field>Unesi ime</v-text-field> -->
      <input v-model="message" placeholder="Unesite ime" style="padding-left:10px;"> 
      <v-btn @click="test(message)">Ok</v-btn>
        </v-layout>
        <div v-if="this.show" style="margin-top:50px;">
          <v-card-title>Unesli ste ime {{ message }}</v-card-title>

            <v-simple-table>
						<thead>Nacionalnost
							<tr>
								<th class="text-left">Country</th>
								<th class="text-left">Probability</th>
							</tr>
						</thead>
						<tbody>
						<tr v-for="x in all.country" :key="x.country_id">
            <td>{{ x.country_id }}</td>
            <td>{{ x.probability }} </td>
            </tr>
						</tbody>
					</v-simple-table>

<v-simple-table style="margin-top:30px;">
						<thead>Godine
							<tr>
								<th class="text-left">Age</th>
								<th class="text-left">Probability</th>
							</tr>
						</thead>
						<tbody>
						<tr>
            <td>{{ this.years.age }}</td>
            <td>{{ this.years.count }} </td>
            </tr>
						</tbody>
					</v-simple-table>

<v-simple-table style="margin-top:30px;">
						<thead>Spol
							<tr>
								<th class="text-left">Count</th>
								<th class="text-left">Gender</th>
								<th class="text-left">Probability</th>
							</tr>
						</thead>
						<tbody>
						<tr>
            <td>{{ this.gender.count }}</td>
            <td>{{ this.gender.gender }} </td>
            <td>{{ this.gender.probability }} </td>
            </tr>
						</tbody>
					</v-simple-table>

        </div>
	</v-container>
</template>

<script>
import axios from "axios";
export default {
	name: "Home",
	data() {
		return {
			all: [],
      years: [],
      gender: [],
      message:"",
      show: false,
		};
		
	},
  methods:{
    async test(message) {
    if(message=='') alert("Niste unesli ime!")
    else{
      console.log(message)
		let temp = await axios.get(`https://api.nationalize.io?name=${this.message}`);
		this.all = temp.data;
    temp = await axios.get(`https://api.agify.io/?name=${this.message}`);
		this.years = temp.data;
    temp = await axios.get(`https://api.genderize.io/?name=${this.message}`);
		this.gender = temp.data;
    console.log("all,", this.all);
     console.log("years,", this.years);
      console.log("gender,", this.gender);

    this.show= true;}
	},
  },
	components: {
	},
};
</script>
