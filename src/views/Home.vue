<template>
  <div class="container">
    <h2 class="text-capitalize pt-5 pb-5">program design</h2>


    <div class="shadow-sm px-5 pb-5 pt-5 card">
      <b-form>
        {{ logic_model }}
        <div class="d-flex bd-highlight">
          <div class="p-2 flex-fill bd-highlight">
            <div>
              <label class="">Please enter the title of your program?</label>
              <b-input v-model="logic_model.program" placeholder="please enter the title of your program"></b-input>

            </div>
          </div>
          <div class="p-2 flex-fill bd-highlight">
            <div>
              <label class="">State Date</label>
              <b-input v-model="start_date" placeholder="E.g. 01/01/2020"></b-input>
            </div>
          </div>
          <div class="p-2 flex-fill bd-highlight">
            <div>
              <label class="">End Date</label>
              <b-input v-model="end_date" placeholder="E.g. 01/01/2020"></b-input>
            </div>
          </div>
        </div>


        <!--    what issues are you trying to solve in this program-->
        <div class="pt-5">
          <label class="">What issues are you trying to solve in this program</label>
          <b-input v-model="problem" @keydown.enter="addProblem" placeholder="Write problem and press enter"></b-input>
          <br>
          <!--          <b-badge  v-for="({name},i) in problems" :key="name" pill variant="primary">{{ name }}</b-badge>-->

          <b-button style="background:none; border:none" variant="primar" v-for="({name},i) in problems" :key="name">

            <b-badge class="pt-1 pb-1" style="border-radius: 100px"> {{ name }} &nbsp;
              <span  @click="removeItem(name)" class="px-2">X</span>

            </b-badge>
          </b-button>
        </div>

        <!--    what are your goals for this program-->


        <div class="pt-5">
          <label class="">What are your goals for this program</label>
          <b-input v-model="goal" @keydown.enter="addGoal" placeholder="Write goals and press enter"></b-input>
          <br>
          <!--          <b-badge  v-for="({name},i) in problems" :key="name" pill variant="primary">{{ name }}</b-badge>-->

          <b-button style="background:none; border:none" variant="primar" v-for="({name},i) in goals" :key="name">

            <b-badge class="pt-1 pb-1" style="border-radius: 100px"> {{ name }} &nbsp;
              <span  @click="removeGoal(name)" class="px-2">X</span>

            </b-badge>
          </b-button>
        </div>
      </b-form>
    </div>

    <!--    SECOND COL-->

    <div class="pt-5">
      <h2 class="text-capitalize pb-3">outcome measurement framework</h2>
      <div class="shadow-sm card px-5 pb-5 pt-2">
        <h4>Inputs</h4>
        <p>What resources are available for this program</p>

        <b-form>
          <!--          personal-->
          <div>
            <b-form-checkbox size="lg">Personal</b-form-checkbox>
            <div class="px-4">
              <label class="">Which personal will be in this program</label>
              <!--              <b-input placeholder="select personal"></b-input>-->
              <b-form-tags
                  v-model="personnels"
              ></b-form-tags>

              <label class="text-muted">Add funding source</label>
              <br>
              <b-button style="background:none; border:none" variant="primar" v-for="val in personnels"
                        :key="val">
                <b-badge class="pt-1 pb-1" style="border-radius: 100px"> {{ val }} &nbsp;
                  <span  @click="removePersonnel(val)" class="px-2">X</span>
                </b-badge>
              </b-button>
            </div>
          </div>

          <!--          Funding-->

          <div class="pt-4">
            <b-form-checkbox size="lg">Funding</b-form-checkbox>
            <div class="px-4">
              <label class="text-muted">Add funding source</label>
              <b-input v-model="Funding" @keydown.enter="addFunding" placeholder="select and press enter"></b-input>
              <br>


              <b-button style="background:none; border:none" variant="primar" v-for="({name},i) in Fundings"
                        :key="name">

                <b-badge class="pt-1 pb-1" style="border-radius: 100px"> {{ name }} &nbsp;
                  <span  @click="removeFunding(name)" class="px-2">X</span>
                </b-badge>
              </b-button>
            </div>
            <!--            -->

            <!--            -->
          </div>
          <!--partnership-->
          <div class="pt-4">
            <b-form-checkbox size="lg">Partnership</b-form-checkbox>
            <div class="px-4">
              <label class="text-muted">Who are also partnering with you in this program?</label>
              <b-input v-model="partnership" @keydown.enter="addpartnership"
                       placeholder="select partner organization"></b-input>
              <br>
              <b-button style="background:none; border:none" variant="primar" v-for="({name},i) in partnerships"
                        :key="name">

                <b-badge class="pt-1 pb-1" style="border-radius: 100px"> {{ name }} &nbsp;

                  <span  @click="removepartnership(name)" class="px-2">X</span>
                </b-badge>
              </b-button>
            </div>

          </div>
          <div class="pt-4">
            <b-form-checkbox size="lg">Other</b-form-checkbox>
            <div class="px-4">
              <label class="text-muted">What other resource you have?</label>
              <b-input v-model="other" @keydown.enter="addOther" placeholder="write and press enter"></b-input>
              <br>
              <b-button style="background:none; border:none" variant="primar" v-for="({name},i) in others"
                        :key="name">

                <b-badge class="pt-1 pb-1" style="border-radius: 100px"> {{ name }} &nbsp;
                  <span  @click="removeOther(name)" class="px-2">X</span>
                </b-badge>
              </b-button>
            </div>

          </div>
        </b-form>
      </div>
    </div>
    <br>
    <br>
    <!--    THRID COL-->

    <div class="pt-2 shadow-sm card">
      <div class="p-2">
        <h4>Activities</h4>
        <p>What activities are you planing to do in this program?</p>
        <div class="row">
          <div class="col-2 py-3" v-for="i in 24" :key="i">
            <b-form-checkbox size="lg">simple service</b-form-checkbox>
          </div>
        </div>
      </div>
    </div>
    <br>
    <br>
    <!--    FOURT-->
    <div class="pt-2 shadow-sm card">
      <div class="px-3 pb-5">
        <h4>Output</h4>
        <p>What are you required to accomplish in this program</p>

        <div class="">
          <label class="text-muted">select your parameters(Number of X)</label>
          <b-input
              v-model="accomplishment"
              @keydown.enter="addAccomplishment"
              placeholder="write and press enter or select from the suggestions"></b-input>
        </div>

        <div
            v-for="a in accomplishments"
            :key="a.id"
            class="d-flex flex-row bd-highlight my-2">
          <div class=" bd-highlight">
            <b-button style="background: lightslategray; border:none">
              {{ a.program_accomplishment_list[0].title }}
            </b-button>
          </div>
          <div class=" bd-highlight px-3">
            <div>
              <b-input placeholder="0"
                       type="text"></b-input>
            </div>
          </div>
          <div class=" bd-highlight pt-1">
            <div>
             <span @click="removeAccomplishment(a)" class="px-2" style="cursor: pointer">X</span>
            </div>
          </div>
        </div>
      </div>
      <!--      -->
    </div>
    <br>
    <br>
    <!--    five col-->
    <!--  measurement OF Achievement    -->
    <div class="pt-5 shadow-sm card ">
      <div class="px-3">
        <h4>Measurement OF Achievement</h4>
        <p>How would you define your success?</p>

        <div class="">
          <label class="text-muted">Select your parameters(Number of X)</label>
          <b-input placeholder="write and press enter or select from the suggestions"></b-input>
        </div>

        <div class="d-flex flex-row bd-highlight mb-3 pt-4">
          <div class=" bd-highlight">
            <b-button style="background: lightslategray; border:none"> Paid participants on field trip</b-button>
          </div>
          <div class=" bd-highlight px-3">
            <div>
              <!--              TODO  change this to b-select-->
              <b-input placeholder="Number"></b-input>
            </div>
          </div>
          <div class=" bd-highlight ">
            <div>
              <div>
                <b-input placeholder="0"></b-input>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="d-flex flex-row bd-highlight mb-3 pt-4 px-3 pb-3">
        <div class=" bd-highlight">
          <b-button style="background: lightslategray; border:none"> Number of animals with freedom from hunger and
            thirsty
          </b-button>
        </div>
        <div class=" bd-highlight px-3">
          <div>
            <b-input placeholder="Percentage"></b-input>
          </div>
        </div>
        <div class=" bd-highlight pt-1">
          <div>
            <b-input placeholder="%"></b-input>
          </div>
        </div>
      </div>
    </div>
    <br>
    <br>
    <!--    sixth col-->
    <!--    outcome-->
    <div class="pt-5 shadow-sm card">
      <div class="px-3 pb-3">
        <h4>What are the intended outcome of your program?</h4>
        <p>How would you define your success?</p>
        <p class="text-danger"> Goal 01: Health Food Supply</p>
        <span class="text-muted">Select measure parameters</span>
        <div>
          <div>
            <b-form-checkbox size="lg">Meet program goal</b-form-checkbox>
          </div>
          <div>
            <b-form-checkbox size="lg">Did not meet program goal</b-form-checkbox>
          </div>

          <div class="d-flex flex-row bd-highlight ">
            <div class=" bd-highlight pt-2">
              <div>
                <b-form-checkbox size="lg">Other</b-form-checkbox>
              </div>
            </div>
            <div class="p-2 bd-highlight">
              <div>
                <b-input placeholder="write"></b-input>
              </div>
            </div>

          </div>
        </div>
      </div>
    </div>

    <div class="pt-5 pb-5">
      <div>
        <h4 class="text-capitalize  pb-3">Global child development program</h4>
      </div>
      <div class="shadow-sm pt-5 card">
        <p class="px-3">The problem we are trying to solve</p>
        <div class="d-flex flex-column bd-highlight mb-3 px-3">
          <div class="p-2 bd-highlight">Child Nutrition</div>
          <div class="p-2 bd-highlight">Child Nutrition</div>
          <div class="p-2 bd-highlight">Child Nutrition</div>
        </div>
      </div>
    </div>
    <div class="pb-3">
      <b-button @click="submit">
        submit
      </b-button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    randId() {
      return Math.random().toString(16).substr(4)
    },

    /**
     *
     */
    submit() {
      const persona = this.personnels.map(p => ({
        name: p,
        individual: this.randId()
      }))


      const {logic_model, start_date, end_date, problems,goals, Fundings, partnerships, accomplishments} = this.$data

      const payload = {
        logic_model, start_date, end_date,
        problems,
        goals,
        Fundings,
        partnerships,
        program_accomplishments: accomplishments,
        personnel: persona,
        "name": "Add",
        "mission": "",
        "type": 1,
      }
      console.log(payload)
      console.log(JSON.stringify(payload))

    },

    addProblem: function () {
      if (!this.problem) {
        return
      }
      this.problems.push({
        name: this.problem,
        id: this.randId()
      })
      this.problem = null
    },

    addGoal: function () {
      if (!this.goal) {
        return
      }
      this.goals.push({
        name: this.goal,
        id: this.randId()
      })
      this.goal = null
      this.name = ""
    },
    //
    addFunding: function () {
      if (!this.Funding) {
        return
      }
      this.Fundings.push({
        name: this.Funding,
        id: this.randId()
      })
      this.Funding = null
      this.name = ""
    },
    addpartnership: function () {
      if (!this.partnership) {
        return
      }
      this.partnerships.push({
        name: this.partnership,
        id: this.randId()
      })
      this.partnership = null
      this.name = ""
    },

    addOther: function () {
      if (!this.other) {
        return
      }
      this.others.push({
        name: this.other,
        id: this.randId()
      })
      this.other = null
      this.name = ""
    },
    /**
     *
     */
    addAccomplishment: function () {
      if (!this.accomplishment) {
        return
      }
      this.accomplishments.push({
        id: this.randId(),
        program_accomplishment_list: [{
          accomplishment_id: this.randId(),
          title: this.accomplishment
        }]
      })
      this.accomplishment = null
    },


    removeItem: function (name) {
      this.problems.splice(this.problems.indexOf(name), 1);
    },
    removeGoal: function (name) {
      this.goals.splice(this.goals.indexOf(name), 1);
    },

    removeFunding: function (name) {
      this.Fundings.splice(this.Fundings.indexOf(name), 1);
    },

    removepartnership: function (name) {
      this.partnerships.splice(this.partnerships.indexOf(name), 1);
    },

    removeOther: function (name) {
      this.others.splice(this.others.indexOf(name), 1);
    },

    removePersonnel: function (val) {
      this.personnels.splice(this.personnels.indexOf(val), 1);
    },

    removeAccomplishment: function (a) {
      this.accomplishments.splice(this.accomplishments.indexOf(a), 1);
    },

  },
  data() {
    return {
      goal:null,
      goals:[],
      Funding: null,
      Fundings: [],
      partnership: null,
      partnerships: [],
      other: null,
      others: [],
      problems: [],
      problem: null,
      start_date: null,
      end_date: null,
      personnels: null,
      accomplishment: null,
      accomplishments: [],
      logic_model: {}
    }
  }
};
</script>

<style lang="scss" scoped></style>
