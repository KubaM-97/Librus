<template>
  <div class="addStudentPanel">
    <div class="addStudentPanelMain">
      <div class="container">
        <div class="row">
          <div class="col-lg-4">
            <form
              action="#"
              enctype="application/x-www-form-urlencoded"
              method="get"
            >
              <div class="addStudentPanelName">
                <label for="name"
                  >*Imię i Nazwisko:
                  <span class="nameTooltip">
                    Podwójne nazwiska przy pomocy myślnika
                  </span>
                </label>

                <input
                  name="#"
                  type="text"
                  v-model.lazy.trim="name"
                  id="name"
                  maxlength="30"
                  autocomplete="off"
                />
                <span class="required">
                  <transition name="bounce">
                    <span class="required" v-if="showError"
                      >Uzupełnij imię i nazwisko</span
                    >
                  </transition>
                </span>
              </div>

              <div class="addStudentPanelNameInfo">
                Informacje dodatkowe
                <span class="showInfo" @click="additionalInfoSwitcher"
                  >Rozwiń</span
                >

                <transition @enter="enter" @leave="leave" :css="false">
                  <div class="info" v-if="info">
                    <div class="form-group">
                      <label for="pesel">PESEL:</label>
                      <input
                        name="#"
                        type="text"
                        v-model.trim="add.pesel"
                        id="Pesel"
                        autocomplete="off"
                        placeholder="PESEL"
                        @keyup="
                          validatorData(
                            'Pesel',
                            '^[0-9]{11}$',
                            'Dokładnie 11 cyfr'
                          )
                        "
                      />
                      <span class="wrongAdditionalInfo" id="wrongPesel"></span>
                    </div>

                    <div class="form-group">
                      <label>Adres:</label>

                      <input
                        name="#"
                        type="text"
                        v-model.trim="add.street.name"
                        id="Street"
                        autocomplete="off"
                        placeholder="ulica"
                        @keyup="
                          validatorData(
                            'Street',
                            '^[0-9a-zA-ZąćęłńóśźżĄĆĘŁŃÓŚŹŻ ]*$',
                            'Bez znaków specjalnych.'
                          )
                        "
                      />
                      <span class="wrongAdditionalInfo" id="wrongStreet"></span>

                      <input
                        name="#"
                        type="text"
                        v-model.trim="add.street.nr"
                        id="HouseNr"
                        autocomplete="off"
                        placeholder="nr_domu"
                        @keyup="
                          validatorData(
                            'HouseNr',
                            '^[0-9]+[a-zA-Z]?(/?[0-9]*[a-zA-Z]?)?$',
                            'Nr, Nr/Nr, Nr Litera <br /> np. 11 11/13 11A 11A/13B'
                          )
                        "
                      />
                      <span
                        class="wrongAdditionalInfo"
                        id="wrongHouseNr"
                      ></span>

                      <input
                        name="#"
                        type="text"
                        v-model.trim="add.street.flat"
                        id="FlatNr"
                        autocomplete="off"
                        placeholder="nr_mieszkania"
                        @keyup="
                          validatorData(
                            'FlatNr',
                            '^[0-9]+[a-zA-Z]?$',
                            'Liczba + ew.litera np.116F'
                          )
                        "
                      />
                      <span class="wrongAdditionalInfo" id="wrongFlatNr"></span>

                      <input
                        name="#"
                        type="text"
                        v-model.trim="add.street.postcode"
                        id="PostCode"
                        autocomplete="off"
                        placeholder="kod pocztowy"
                        @blur="
                          validatorData(
                            'PostCode',
                            '^[0-9]{2}-[0-9]{3}$',
                            '_ _ - _ _ _'
                          )
                        "
                      />
                      <span
                        class="wrongAdditionalInfo"
                        id="wrongPostCode"
                      ></span>

                      <input
                        name="#"
                        type="text"
                        v-model.trim="add.street.city"
                        id="City"
                        autocomplete="off"
                        placeholder="miasto"
                        @keyup="
                          validatorData(
                            'City',
                            '^[A-ZĄĆĘŁŃÓŚŹŻ][a-ząćęłńóśźż]*( (- )?[A-ZĄĆĘŁŃÓŚŹŻ][a-ząćęłńóśźż]*)*$',
                            'Brak Cyfr i znaków specjalnych. <br />'
                          )
                        "
                      />
                      <span class="wrongAdditionalInfo" id="wrongCity"></span>
                    </div>

                    <div class="form-group">
                      <label for="Phone">Telefon:</label>
                      <input
                        name="#"
                        type="text"
                        v-model.trim="add.phone"
                        id="Phone"
                        autocomplete="off"
                        placeholder="Telefon"
                        @blur="
                          validatorData(
                            'Phone',
                            '^([0-9]{7}|[0-9]{9})$',
                            'Dokładnie 7 lub 9 cyfr.'
                          )
                        "
                      />
                      <span class="wrongAdditionalInfo" id="wrongPhone"></span>
                    </div>

                    <div class="form-group">
                      <label for="Email">Email:</label>
                      <input
                        name="#"
                        type="text"
                        v-model.trim="add.email"
                        id="Email"
                        autocomplete="off"
                        placeholder="adres e-mail"
                        @blur="
                          validatorData(
                            'Email',
                            '^[a-zA-Z0-9-_\.]+@[a-zA-Z0-9-]+\.[a-z]+$',
                            'nazwa@domena.pl'
                          )
                        "
                      />
                      <span class="wrongAdditionalInfo" id="wrongEmail"></span>
                    </div>

                    <div class="parents">
                      <div class="mother">
                        <div class="form-group">
                          <label>Matka:</label>

                          <input
                            name="#"
                            type="text"
                            v-model.trim="add.mother.firstName"
                            id="MothersFirstName"
                            autocomplete="off"
                            placeholder="Imię matki"
                            @keyup="
                              validatorData(
                                'MothersFirstName',
                                '^[A-ZĄĆĘŁŃÓŚŹŻ][a-ząćęłńóśźż]*( [A-ZĄĆĘŁŃÓŚŹŻ][a-zząćęłńóśźż]*)?$',
                                'Brak cyfr i znaków specjalnych. <br /><br /> Możliwe drugie imię <br />np. Anna Maria'
                              )
                            "
                          />
                          <span
                            class="wrongAdditionalInfo"
                            id="wrongMothersFirstName"
                          ></span>

                          <input
                            name="#"
                            type="text"
                            v-model.trim="add.mother.lastName"
                            id="MothersLastName"
                            autocomplete="off"
                            placeholder="Nazwisko matki"
                            @keyup="
                              validatorData(
                                'MothersLastName',
                                '^[A-ZĄĆĘŁŃÓŚŹŻ][a-ząćęłńóśźż]*(-[A-ZĄĆĘŁŃÓŚŹŻ][a-ząćęłńóśźż]*)?$',
                                'Brak cyfr i znaków specjalnych. <br /><br />Możliwe drugie nazwisko po myślniku <br />np. Ćwierć-Parzącha'
                              )
                            "
                          />
                          <span
                            class="wrongAdditionalInfo"
                            id="wrongMothersLastName"
                          ></span>

                          <input
                            name="#"
                            type="text"
                            v-model.trim="add.mother.phone"
                            id="MothersTelephone"
                            autocomplete="off"
                            placeholder="numer telefonu matki"
                            @blur="
                              validatorData(
                                'MothersTelephone',
                                '^[0-9]{7}([0-9]{2})?$',
                                'Dokładnie 7 lub 9 cyfr.'
                              )
                            "
                          />
                          <span
                            class="wrongAdditionalInfo"
                            id="wrongMothersTelephone"
                          ></span>

                          <input
                            name="#"
                            type="text"
                            v-model.trim="add.mother.email"
                            id="MothersEmail"
                            autocomplete="off"
                            placeholder="email matki"
                            @blur="
                              validatorData(
                                'MothersEmail',
                                '^[a-zA-Z0-9-_\.]+@[a-zA-Z0-9-]+\.[a-z]+$',
                                'nazwa@domena.pl'
                              )
                            "
                          />
                          <span
                            class="wrongAdditionalInfo"
                            id="wrongMothersEmail"
                          ></span>
                        </div>
                      </div>

                      <div class="father">
                        <div class="form-group">
                          <label>Ojciec:</label>

                          <input
                            name="#"
                            type="text"
                            v-model.trim="add.father.firstName"
                            id="FathersFirstName"
                            autocomplete="off"
                            placeholder="Imię ojca"
                            @keyup="
                              validatorData(
                                'FathersFirstName',
                                '^[A-ZĄĆĘŁŃÓŚŹŻ][a-ząćęłńóśźż]*( [A-ZĄĆĘŁŃÓŚŹŻ][a-ząćęłńóśźż]*)?$',
                                'Brak cyfr i znaków specjalnych. <br /><br /> Możliwe drugie imię <br />np. Jan Maria'
                              )
                            "
                          />
                          <span
                            class="wrongAdditionalInfo"
                            id="wrongFathersFirstName"
                          ></span>

                          <input
                            name="#"
                            type="text"
                            v-model.trim="add.father.lastName"
                            id="FathersLastName"
                            autocomplete="off"
                            placeholder="Nazwisko ojca"
                            @keyup="
                              validatorData(
                                'FathersLastName',
                                '^[A-ZĄĆĘŁŃÓŚŹŻ][a-ząćęłńóśźż]*(-[A-ZĄĆĘŁŃÓŚŹŻ][a-ząćęłńóśźż]*)?$',
                                'Brak cyfr i znaków specjalnych. <br /><br />Możliwe drugie nazwisko po myślniku <br />np. Ćwierć-Parzącha'
                              )
                            "
                          />
                          <span
                            class="wrongAdditionalInfo"
                            id="wrongFathersLastName"
                          ></span>

                          <input
                            name="#"
                            type="text"
                            v-model.trim="add.father.phone"
                            id="FathersTelephone"
                            autocomplete="off"
                            placeholder="numer telefonu ojca"
                            @blur="
                              validatorData(
                                'FathersTelephone',
                                '^[0-9]{7}([0-9]{2})?$',
                                'Dokładnie 7 lub 9 cyfr.'
                              )
                            "
                          />
                          <span
                            class="wrongAdditionalInfo"
                            id="wrongFathersTelephone"
                          ></span>

                          <input
                            name="#"
                            type="text"
                            v-model.trim="add.father.email"
                            id="FathersEmail"
                            autocomplete="off"
                            placeholder="email ojca"
                            @blur="
                              validatorData(
                                'FathersEmail',
                                '^[a-zA-Z0-9-_\.]+@[a-zA-Z0-9-]+\.[a-z]+$',
                                'nazwa@domena.pl'
                              )
                            "
                          />
                          <span
                            class="wrongAdditionalInfo"
                            id="wrongFathersEmail"
                          ></span>
                        </div>
                      </div>
                    </div>
                  </div>
                </transition>
              </div>
            </form>
          </div>

          <div class="col-lg-8 addStudentPanelGrades">
            <div class="addStudentPanelGradesTitle">
              <span class="addStudentGradeSubpanelTitle"
                >Dotychczasowe oceny:</span
              >
            </div>

            <div
              class="addStudentPanelGradesContent"
              v-for="(n, index) in gradesLength"
              :key="n"
            >
              <grade-component
                :index="index"
                v-model:gradesLength="gradesLength"
              ></grade-component>
            </div>

            <div class="showAnotherGrade">
              <button name="moreGradesAddStudent" @click="gradesLength++">
                +
              </button>
            </div>
          </div>
        </div>

        <div class="row">
          <div class="addStudentPanelSummary">
            <table class="summary">
              <tr>
                <td>
                  <span v-if="name !== ''">{{ formatName(name) }}</span>
                </td>

                <td ref="allnewGrades">
                  <span
                    class="grades"
                    v-html="gradeWeightColor(marks, weights)"
                  >
                  </span>
                </td>

                <td>
                  <span>
                    {{ avg(marks, weights) }}
                  </span>
                </td>

                <td>
                  <span v-html="threatness(avg(marks, weights))"> </span>
                </td>
              </tr>
            </table>
          </div>
        </div>

        <div class="row">
          <div class="addStudentPanelButtons">
            <button
              name="addStudentCancel"
              class="btn btn-danger btn-lg"
              @click="addStudentCancel()"
            >
              Anuluj
            </button>

            <button
              name="addStudent"
              class="btn btn-primary btn-lg"
              @click="addStudentToClass()"
            >
              Dodaj ucznia
            </button>
          </div>
        </div>
      </div>
    </div>
    <teleport to="body">
      <div class="confirm" v-show="confirm">
        <p>Na pewno? Dane zostaną utracone...</p>
        <button name="showConfirmQuit" @click="showConfirmWindow('quit')">
          Wychodzę
        </button>
        <button name="showConfirmStay" @click="showConfirmWindow('stay')">
          Racja, zostaję!
        </button>
      </div>
    </teleport>
  </div>
</template>



<script>
import dataService from "../assets/mixins/dataMixins.js";
import gradesService from "../assets/mixins/gradesMixins.js";

import { ref, computed, onUpdated, onBeforeMount, onMounted } from "vue";

import { onBeforeRouteLeave, useRouter } from "vue-router";
import { useStore } from "vuex";

import Grade from "./Grade.vue";

export default {
  name: "AddStudent",
  components: {
    "grade-component": Grade,
  },
  setup() {

    const router = useRouter();

    const store = useStore();
    const gradesVuex = store.state.newGrades;

    const students = computed(() => store.state.students);

    const add = {
      id: "",
      lastName: "",
      firstName: "",
      marks: "",
      weights: "",
      descriptions: "",
      dates: "",
      pesel: "",
      street: {
        name: "",
        nr: "",
        flat: "",
        postcode: "",
        city: "",
      },
      phone: "",
      email: "",
      mother: {
        firstName: "",
        lastName: "",
        phone: "",
        email: "",
      },
      father: {
        firstName: "",
        lastName: "",
        phone: "",
        email: "",
      },
    };

    const name = ref("");
    const info = ref(false);
    const confirm = ref(false);
    const exitPath = ref("");
    const block = ref(true);
    const showError = ref(false);
    const gradesLength = ref(1);

    const marks = computed(() => gradesVuex.marks);
    const weights = computed(() => gradesVuex.weights);
    const descriptions = computed(() => gradesVuex.descriptions);

    //converts student's full name to correct form
    //e.g jan kowalski => KOWALSKI Jan
    function formatName(name) {
      const wrongName = document.querySelector(".required");
      const reg = new RegExp(
        "^[A-ZĄĆĘŁŃÓŚŹŻ]?[a-ząćęłńóśźż]*( [A-ZĄĆĘŁŃÓŚŹŻ]?[a-ząćęłńóśźż]*)+(-[A-ZĄĆĘŁŃÓŚŹŻ]?[a-ząćęłńóśźż]+)?$"
      );

      if (reg.test(name)) {
        wrongName.innerHTML = "";
        const fullName = [];

        //splits name into firstName and lastName
        //e.g jan kowalski => ["jan", "kowalski"]
        const nameArray = name.split(" ");
        const firstName = nameArray[0];
        firstName.toLowerCase();

        //splits firstName and lastName into single letters
        //e.g jan => ["j", "a", "n"]
        const singleLetter = firstName.split("");

        //makes the first letter bigger
        //e.g jan[0] => ["j"] => ["J"]
        const bigFirstLetter = singleLetter[0].toUpperCase();

        //replaces firts small letter of firstName to Big letter
        //e.g jan => Jan
        fullName.push(firstName.replace(singleLetter[0], bigFirstLetter));

        if (nameArray.length > 1) {
          //replaces lastname to BIG LETTERS
          //e.g kowalski => KOWALSKI
          const lastName = nameArray[1];
          fullName.push(lastName.toUpperCase());

          add.firstName =
            firstName.charAt(0).toUpperCase() + firstName.slice(1);
          add.lastName = lastName.charAt(0).toUpperCase() + lastName.slice(1);
        }

        //converts array into string
        return fullName.reverse().join(" ");
      } else {
        wrongName.innerHTML = "Bez cyfr i znaków specjalnych.";
      }
    }

    onBeforeRouteLeave((to, _, next) => {
      if (to.path == "/LoggedOut") {
        addStudentCancel();
        next();
      } else {
        let i = 0;
        do {
          //if
          // 1. a grade has a mark but doesn`t have a weight
          // 2. a grade doesn`t have a mark but has a weight
          // 3. there is neither a mark nor a weight but there is a description
          // 4. there is no name but there is at least one mark, one weight or one description
          if((     ((marks.value[i])&&(!weights.value[i]))
              || ((!marks.value[i])&&(weights.value[i]))
              || ((!marks.value[i])&&(!weights.value[i])&&(descriptions.value[i]))
              || ((!name.value)&&((marks.value[i])||(weights.value[i])||(descriptions.value[i])))
            )
              && (block.value==true)){
            exitPath.value = to.path;
            confirm.value = true;
            next(false);
            
          } else {
            addStudentCancel();
            block.value = true;
            next();
          }
          i++;
        } while (i <= marks.length);
      }
    });

    onUpdated(() => {
      for (let i = 0; i < marks.value.length; i++) {
        gradesService().showTooltip(document, gradesVuex);
      }
    });

    onBeforeMount(() => {
      for (const gradeProperty in gradesVuex) {
        gradesVuex[gradeProperty] = [];
      }
    });

    onMounted(() => {
      if (name != "") {
        const arrName = name.value.split(" ");
        add.firstName = arrName[0];
        add.lastName = arrName[1];
      }

      for (let i = 0; i < marks.length; i++) {
        gradeService().showTooltip(document, this);
      }
    });

    //starts animation of Student's detail data
    function enter(el, done) {
      el.addEventListener("animationend", function () {
        el.style = "";
        done();
      });
      el.style.animation = "showDetailData 1s";
    }

    //ends animation of Student's detail data
    function leave(el, done) {
      el.addEventListener("animationend", function () {
        el.style = "";
        done();
      });
      el.style.animationName = "showDetailData";
      el.style.animationDuration = "1s";
      el.style.animationDirection = "reverse";
    }

    //shows additional information
    function additionalInfoSwitcher() {

      const spanInfoSwitcher = document.querySelector(".addStudentPanelNameInfo span.showInfo");
      info.value = !info.value;
      spanInfoSwitcher.innerHTML == "Rozwiń" ? (spanInfoSwitcher.innerHTML = "Zwiń")   : (spanInfoSwitcher.innerHTML = "Rozwiń");

    }

    //shows confirm window
    function showConfirmWindow(action) {
      if (action == "quit") {
        block.value = false;
        router.push({ path: exitPath.value });
      } else if (action == "stay") {
        confirm.value = false;
        exitPath.value = "";
      }
    }

    //resets addStudent Panel
    function addStudentCancel() {
      name.value = "";

      for (const gradeProperty in gradesVuex) {
        gradesVuex[gradeProperty] = [];
      }

      gradesLength.value = 1;
    }

    //adds a new student to the class table
    function addStudentToClass() {
      //this is inserted by user (by teacher) name for a new student
      const addedStudentName = name.value;

      //splits name into firstname and lastname
      const addedStudentNameArray = addedStudentName.split(" ");

      //if we've got both firstname and lastname
      if (addedStudentNameArray.length >= 2) {
        getRidOfEmptyGrades();

        add.id = students.value.length + 1;

        for (const gradeProperty in gradesVuex) {
          add[gradeProperty] = gradesVuex[gradeProperty];
        }

        store.state.students[store.state.students.length] = add;

        block.value = false;
        router.push({ name: "FullClass" });
      } else {
        showError.value = true;

        if (showError.value == true) {
          showError.value = false;

          setTimeout(() => {
            showError.value = true;
          }, 10);
        }
      }
    }

    //removes grades that have marks but don`t have weights or don`t have marks but have weights
    function getRidOfEmptyGrades() {

      for (let i = marks.value.length - 1; i >= 0; i--) {

        const m = marks.value[i];
        const w = weights.value[i];

        if ( (m !== "" && w === "") || (m === "" && w !== "") || (m === "" && w === "") ) {

          for (const gradeProperty in gradesVuex) {
            gradesVuex[gradeProperty].splice(i, 1);
          }

        }

      }

    }

    return {
      marks,
      weights,
      add,
      name,
      info,
      confirm,
      showError,
      gradesLength,
      formatName,
      enter,
      leave,
      additionalInfoSwitcher,
      showConfirmWindow,
      addStudentCancel,
      addStudentToClass,
      ...dataService(),
      ...gradesService(),
    };
  },
};
</script>



<style scoped>
.addStudentPanel {
  width: 90%;
  max-width: 1400px;
  margin: 100px auto;
  -webkit-box-shadow: 3px 3px 30px 5px #00c3ff;
  -moz-box-shadow: 3px 3px 30px 5px #00c3ff;
  box-shadow: 3px 3px 30px 5px #00c3ff;
  background-color: rgba(0, 0, 0, 0.55);
  text-align: center;
  font-size: 11px;
}
.addStudentPanelMain {
  padding: 40px 5px;
}
.addStudentPanelName {
  margin-top: 80px;
  height: 160px;
}
.addStudentPanelName input {
  outline: none;
  display: block;
  margin: 10px auto;
  text-align: center;
  background-color: black;
  border-radius: 5px;
  border: 1px solid #ddd;
  box-sizing: border-box;
  text-shadow: none;
  width: 65%;
  font-size: 12px;
}
.addStudentPanelName input:focus {
  border: 2px solid #a5cda5;
  -webkit-box-shadow: 0px 0px 10px 2px rgba(204, 204, 204, 0.9);
  -moz-box-shadow: 0px 0px 10px 2px rgba(204, 204, 204, 0.9);
  box-shadow: 0px 0px 10px 2px rgba(204, 204, 204, 0.9);
}
.addStudentPanelName span.nameTooltip {
  font-size: 9px;
  display: block;
}
.addStudentPanelName span.required {
  display: block;
  font-size: 11px;
  color: white;
  text-shadow: 5px 0px 5px #f0351d, -5px 0px 5px #f0351d, 0px 5px 5px #f0351d,
    0px -5px 5px #f0351d;
}
.addStudentPanelNameInfo {
  margin-bottom: 50px;
}
.addStudentPanelNameInfo span.showInfo {
  cursor: pointer;
  font-size: 9px;
  margin-left: 25px;
}
.addStudentPanelNameInfo div.info {
  margin-top: 50px;
}
.addStudentPanelNameInfo .form-group {
  width: 100%;
  display: inline-block;
  vertical-align: top;
}
.addStudentPanelNameInfo label {
  float: left;
  padding-left: 25px;
  margin-top: 15px;
  font-size: 12px;
}
.addStudentPanelNameInfo input {
  display: block;
  float: right;
  width: 50%;
  margin-right: 50px;
  background-color: black;
  border: 0.2px solid white;
  border-top: none;
  border-left: none;
  border-right: none;
  box-shadow: 2px 2px 0px 0px white;
  text-align: left;
  padding-left: 15px;
  text-shadow: none;
  font-size: 12px;
}
.addStudentPanelNameInfo span[class^="wrong"] {
  font-size: 11.5px;
  display: block;
  width: 60%;
  float: right;
  margin-right: 30px;
  margin-top: 11px;
}
.addStudentPanelGrades {
  position: relative;
}
.addStudentPanelGradesTitle {
  padding-top: 10px;
  margin-bottom: 50px;
  font-size: 11px;
}
.addStudentPanelGradesContent {
  width: 90%;
}
.showAnotherGrade {
  position: absolute;
  top: 10px;
  right: 15px;
}

.addStudentPanelSummary {
  width: 90%;
  margin: 100px 70px 0;
}
.addStudentPanelButtons {
  width: 90%;
  text-align: right;
  margin-top: 50px;
}
.addStudentPanelButtons button {
  font-size: 14px;
  padding: 8px 12px;
  margin-left: 25px;
}
.confirm {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 15px;
  width: 500px;
  max-width: 80%;
  height: 200px;
  padding-top: 50px;
  background-color: black;
  box-shadow: 3px 3px 30px 5px #00c3ff;
  text-align: center;
}
.confirm p {
  margin-bottom: 50px;
}
.confirm button {
  padding: 10px;
  color: white;
  margin: 0 30px;
  border-radius: 10px;
}
.confirm button:first-of-type {
  background-color: red;
}
.confirm button:last-of-type {
  background-color: green;
}

@media (max-width: 768px) {
  .addStudentPanelMain {
    padding: 40px 10px;
  }
  .addStudentPanelName {
    margin-bottom: 0px;
  }
  .addStudentPanelName span.required {
    height: 40px;
  }
  .addStudentPanelNameInfo input {
    margin-right: 0px;
  }
  .addStudentPanelNameInfo span[class^="wrong"] {
    margin-right: 0px;
  }
  .addStudentPanelGradesTitle {
    padding-top: 70px;
  }
  .showAnotherGrade {
    top: 35px;
    right: 10px;
  }
  .showAnotherGrade button {
    font-size: 19px;
    padding: 1px 9px;
    font-weight: 300;
  }
  .addStudentPanelSummary {
    width: 100%;
    margin: 100px 0;
  }
  .confirm button {
    margin: 0 20px;
  }
}
</style>
