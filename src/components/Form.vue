<template>
    <div id="main">
        <div class="formField">
            <label>Name</label>
            <br />
            <input type="text" v-model="name" />
        </div>
        <div class="formField">
            <label> Last name</label>
            <br />
            <input type="text" v-model="lastName" />
        </div>
        <div class="formField">
            <label>Date of Birth</label>
            <br />
            <input type="date" :max="getDate()" v-model="dateOfBirth" />
        </div>
        <div class="formField">
            <label>Email or Phone</label>
            <br />
            <input id="emailField" class="inputField" type="text" v-model="emailPhone" @blur="verifyType()" />
        </div>

        <!-- when new field is add this FOR will detect it and show -->
        <div class="formField" v-for="(field, idx) in newFields" :key="idx">
            <label>{{ field.newFieldName }}</label>
            <br />
            <input class="inputField" :type="field.newFieldType" v-model="newFieldsValue[idx]" />
        </div>

        <div id="preNewField" v-if="addField">
            <div id="newField">
                <div class="formField">
                    <label>New Field Name</label>
                    <input type="text" v-model="newFieldName" />
                </div>

                <label>Type</label>
                <div id="typeField">
                    <div class="typeFieldChild">
                        <div style="display: flex; flex-direction: row">
                            <input name="newField" type="radio" v-model="newFieldType" value="text" />
                            <label for="css">TEXT</label>
                        </div>
                        <div style="display: flex; flex-direction: row">
                            <input name="newField" type="radio" v-model="newFieldType" value="checkbox" />
                            <label for="css">CHECK-BOX</label>
                        </div>
                        <div style="display: flex; flex-direction: row">
                            <input name="newField" type="radio" v-model="newFieldType" value="color" />
                            <label for="css">COLOR</label>
                        </div>
                        <div style="display: flex; flex-direction: row">
                            <input name="newField" type="radio" v-model="newFieldType" value="date" />
                            <label for="css">DATE</label>
                        </div>
                        <div style="display: flex; flex-direction: row">
                            <input name="newField" type="radio" v-model="newFieldType" value="email" />
                            <label for="css">EMAIL</label>
                        </div>
                    </div>

                    <div class="typeFieldChild">
                        <div style="display: flex; flex-direction: row">
                            <input name="newField" type="radio" v-model="newFieldType" value="file" />
                            <label for="css">FILE</label>
                        </div>
                        <div style="display: flex; flex-direction: row">
                            <input name="newField" type="radio" v-model="newFieldType" value="password" />
                            <label for="css">PASSWORD</label>
                        </div>
                        <div style="display: flex; flex-direction: row">
                            <input name="newField" type="radio" v-model="newFieldType" value="radio" />
                            <label for="css">RADIO</label>
                        </div>
                        <div style="display: flex; flex-direction: row">
                            <input name="newField" type="radio" v-model="newFieldType" value="range" />
                            <label for="css">RANGE</label>
                        </div>
                        <div style="display: flex; flex-direction: row">
                            <input name="newField" type="radio" v-model="newFieldType" value="image" />
                            <label for="css">IMAGE</label>
                        </div>
                    </div>
                </div>
                <button @click="addNewField(); addField = false">OK</button>
            </div>
        </div>

        <div id="formButtons">
            <button @click="addField = true">ADD NEW FIELD</button>
            <button @click="getForm">ENVIAR</button>
        </div>
    </div>

    <div v-if="sendValidate">
        {{ getForm() }}
    </div>
</template>

<script>
export default {
    data() {
        return {
            bgImg: "",
            name: "",
            lastName: "",
            dateOfBirth: "",
            emailPhone: "",
            addField: false,
            newFieldName: "",
            newFieldType: "",
            newFields: [],
            newFieldsValue: [],
            sendValidate: false,
        };
    },
    methods: {
        getDate() {
            return new Date().toISOString().slice(0, 10);
        },

        verifyType() {
            let reg = new RegExp("[0-9]");
            let mail = false;
            let phone = this.emailPhone;
            phone = phone.split("");
            for (let i = 0; i < phone.length; i++) {
                if (phone[i] == " " || phone[i] == "(" || phone[i] == ")" || phone[i] == "-") {
                    phone.splice(i, 1);
                    i--;
                } else if (!reg.test(phone[i])) {
                    mail = true;
                    this.bgImg = "email";
                    break;
                }
            }

            if (!mail) {
                this.emailPhone = "";
                this.bgImg = "phone-call";
                for (let i = 0; i < phone.length; i++) {
                    if (i == 0) this.emailPhone = `(${phone[i]}`;
                    else if (i == 1) this.emailPhone += `${phone[i]}) `;
                    else if (phone.length - i == 5) this.emailPhone += `${phone[i]}-`;
                    else this.emailPhone += `${phone[i]}`;
                }
            }

            if (this.emailPhone == "") {
                this.bgImg = "";
            }

            let el = document.getElementById("emailField");

            if (el.classList.contains("email" || "phone-call")) {
                el.classList.remove("email");
                el.classList.remove("phone-call");
            }

            if (this.bgImg) {
                el.classList.add(this.bgImg);
            }
        },

        getForm() {
            for (let i = 0; i < this.newFields.length; i++) {
                this.newFields[i].newFieldValue = this.newFieldsValue[i];
            }

            const formObj = {
                name: this.name,
                lastName: this.lastName,
                dateOfBirth: this.dateOfBirth,
                emailPhone: this.emailPhone,
                newFields: this.newFields,
            };
            this.sendValidate = true;

            return formObj;
        },
        addNewField() {
            this.newFields.push({
                newFieldName: this.newFieldName,
                newFieldType: this.newFieldType,
                newFieldValue: "",
            });
        },
    },
};
</script>

<style scoped>
#main {
    display: flex;
    flex-direction: column;
    max-width: 400px;
    width: 90%;
    margin: auto;
    font-weight: 600;
}

.formField {
    width: 100%;
}

.formField input {
    width: 100%;
    border: none;
    height: 32px;
    border-radius: 0.4rem;
    outline: none;
    margin: 10px 0;
    padding: 2px 0 2px 8px;
    font-weight: 300;
}

#emailPhoneContainer {
    display: flex;
    align-items: center;
}

#emailPhoneContainer * {
    border: none;
}

#emailField {
    background-repeat: no-repeat;
    background-position: calc(100% - 10px);
    background-size: 32px;
    border-radius: 0.4rem;
}

.phone-call {
    background-image: url("../assets/phone-call.png");
}

.email {
    background-image: url("../assets/email.png");
}

#main button {
    margin: 15px auto;
    width: 50%;
    height: 35px;
    border-radius: 0.4rem;
    transition: all 0.4s;
    border: none;
    outline: none;
}

#main button:hover {
    cursor: pointer;
    box-shadow: #fff 0px 0px 5px;
}

#preNewField {
    margin: 15px auto;
    box-shadow: white 0px 0px 10px;
    outline: rgb(197, 197, 197) 2px solid;
    border-radius: 0.4rem;
    padding: 10px;
}
#newField {
    margin: auto;
    width: 90%;
    padding-right: 10px;
}

#typeField {
    margin: 15px 0;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-end;
}

.typeFieldChild {
    width: 100%;
}

#formButtons {
    display: flex;
    flex-direction: row;
    transition: all 0.2s;
}

#formButtons button {
    width: 45%;
    font-weight: 600;
}

@media screen and (max-width: 768px) {
    #formButtons {
        display: flex;
        flex-direction: column;
    }
}
</style>




