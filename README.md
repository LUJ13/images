Hi guys,

<a name="home">Thanks for reading the README</a>

1. [ElementUI design and Demo introduction](#ch1)
2. [Installation guide and component introduction](#ch2)
3. [Function introduction](#ch3)  

    - [LoginView.vue-Login page](#ch3_1)  
    - [HomeView.vue-Home page](#ch3_2)
    - [IndexView.vue-Loan apply page](#ch3_3)
    - [IndexView.vue-Loan apply management](#ch3_4)
    
4. [Reference](#ref)

***
## <a name="ch1">ElementUI design and demo introduction</a> 
ElementUI design is based on the Vue version of 2.X,if you want to learn the Vue 3.0, you may need to cheak the Element Plus for details.For developers, efficient, simple and easy-to-use development is the best.Streamlining the process of developing UI/UX frameworks as a developer, such as ElementUI Design, is not an option.

The demonstration will focus on the part of Loan Back-office mangement: `Login` ，`Loan apply creation` and `Loan management`.Assuming that a user applies for a loan, then any business that issues loans needs to have a backend operating software that approves the user's basic information, and through different levels of approvals, ultimately completes the issuance of the loan. If you want to complete this design in a short period of time, then ElementUI combined with Vue2.X meets this need, the following is the login interface of the site.
![prototyping](https://github.com/LUJ13/images/blob/main/Login.png?raw=true)


## <a name="ch2">Installation guide</a> 
If you want to start developing, the first thing is install the vue  `npm install vue `,the next steps is to install the  `npm install element-ui`
```
npm install vue@2
npm i element-ui -S 
```
### Steps to run the Loan back-office management application
1. Download the repository into your local environment
2. Open the visual studio code,then choose the `open Folder`
3. Run the application by `npm run serve` and the application should be ready in `http://localhost:8080/` and wait for testing.
## <a name="ch3">Function introduction</a>
### <a name="ch3_1">LoginView.vue-Login page</a>
It shows how to use the Element UI component in the `template` section of a Vue component to create a form with username and password input boxes and a submit button.Because I'm using the real interface documentation, the username and password are fixed.The username is`admin`and `approve123456.`is the password.

```
<template>
  <div class="login-box">
    <div class="login-input-box">
      <h1>Loan back-office management</h1>
      <el-form
        :model="ruleForm"
        :rules="rules"
        status-icon
        ref="ruleForm"
        class="demo-ruleForm"
      >
        <el-form-item prop="username">
          <el-input
            prefix-icon="el-icon-user-solid"
            v-model="ruleForm.username"
          ></el-input>
        </el-form-item>

        <el-form-item prop="pass">
          <el-input
            prefix-icon="el-icon-s-order"
            type="password"
            v-model="ruleForm.pass"
            autocomplete="off"
          ></el-input>
        </el-form-item>

        <el-button type="primary" @click="submitForm">Submit</el-button>
      </el-form>
    </div>
  </div>
</template>
```
When the username and password are entered correctly, the home page of the management system will be accessed.
![prototyping](https://github.com/LUJ13/images/blob/main/5.png?raw=true)
At the same time, there is a logout button in the upper right corner to return directly to the login screen.
![prototyping](https://github.com/LUJ13/images/blob/main/2.png?raw=true)

### <a name="ch3_2">HomeView.vue-Home page</a>
The upper part is divided into 4 parts using the raster mode, and the lower part is inserted with 3 E-charts, Line chart,Bar chart,Pie chart respectively.Ues the `<el-row>` and `a<el-col>` .The data in it is not compatible with this topic and is used for testing purposes and can be subsequently modified according to requirements.
```
<template>
  <div class="home">
    <el-row :gutter="10">
      <el-col
        :xl="6"
        :lg="6"
        :md="12"
        :sm="24"
        :xs="24"
        v-for="(item, index) in list"
        :key="index"
      >
        <div class="dashboard-item" :style="{ background: item.color }">
          <p>{{ item.title }}</p>
          <countTo :startVal="0" :endVal="item.val" :duration="3000"></countTo>
        </div>
      </el-col>
    </el-row>
    <!-- echarts table-->
    <div class="echarts-box">
      <div class="chart1"></div>
      <div class="chart2"></div>
      <div class="chart3"></div>
    </div>
  </div>
</template>
```
Breadcrumb navigation example built using Vue and Element UI, mainly used to display the user's current location path in a web application. Shows how to use Element UI's breadcrumb component in the `<template>` section of a Vue component, and how to combine it with a Vue Router for page jumping.`<el-submenu>``<el-menu-item>`indicates different levels of navigation,it is like a father-son relationship.`<router-link>`implemented jumps between pages.
```
<template>
    <div>
        <el-container>
             <el-aside width="240px">
            <el-menu   class="el-menu-vertical-demo" background-color="#545c64"
                text-color="#fff" active-text-color="#ffd04b">
                 <el-menu-item index="1">
                    <span slot="title"> 
                        <router-link to="/home">Home</router-link>
                    </span>
                 </el-menu-item>
                <el-submenu index="2">
                        <template slot="title">
                        <span>Loan Mangement</span>
                        </template>
                      <el-menu-item index="2-1">
                         <router-link to="/loan-input/index">Loan Apply</router-link>
                      </el-menu-item>
                </el-submenu>  
                <el-submenu index="3">
                        <template slot="title">
                        <span>Apply Mangement</span>
                        </template>
                      <el-menu-item index="3-1">
                         <router-link to="/application-manage/index">Apply list</router-link>
                      </el-menu-item>
                </el-submenu>
                <el-submenu index="4">
                        <template slot="title">
                        <span>loan Approval </span>
                        </template>
                      <el-menu-item index="4-1">
                         <router-link to="/loan-approve/first">Fisrt Approval</router-link>
                      </el-menu-item>
                      <el-menu-item index="4-2">
                         <router-link to="/loan-approve/end">Final Approval</router-link>
                      </el-menu-item>
                </el-submenu>
                
            </el-menu>

</el-aside>
            <el-container>
                <el-header>
               
               <div class="left">
                   <breadcrumb />
                </div>
     			
                <div class="right">
                   
                   <el-dropdown @command="logout">
                       
                    <span class="el-dropdown-link"> admin </span>
                       
                    <el-dropdown-menu slot="dropdown">
                        <el-dropdown-item command="logout">Login out</el-dropdown-item>
                    </el-dropdown-menu>
                       
                  </el-dropdown>
                </div>
 </el-header>

                <el-main>
                    <router-view/>
                </el-main>

            </el-container>
        </el-container>
    </div>
</template>
```
![prototyping](https://github.com/LUJ13/images/blob/main/3.png?raw=true)
### <a name="ch3_3">IndexView.vue-Loan apply page</a>
The loan application interface is divided into 5 sections, using `<el-card>` and `<el-form>`, where `:xl="8" :lg="8" :md="12" :sm="24" :xs="24"` is to adapt to screen scaling.I show one of the cards.A validation of the information is done at creation time, and the data is cleared at reset time.
```
<el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>Personal Information</span>
        </div>
        <el-row>
          <el-col :xl="8" :lg="8" :md="12" :sm="24" :xs="24">
            <el-form-item label="Name" prop="name">
              <el-input type="input" v-model="form.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :xl="8" :lg="8" :md="12" :sm="24" :xs="24">
            <el-form-item label="Birthday" prop="birthday">
              <el-date-picker
                v-model="form.birthday"
                type="date"
                placeholder="Select the date"
              >
              </el-date-picker>
            </el-form-item>
          </el-col>

          <el-col :xl="8" :lg="8" :md="12" :sm="24" :xs="24">
            <el-form-item label="Sex" prop="sex">
              <el-select placeholder="Select sex" v-model="form.sex">
                <el-option key="man" label="Man" value="man"> </el-option>
                <el-option key="woman" label="Woman" value="woman"> </el-option>
              </el-select>
            </el-form-item>
          </el-col>

          <el-col :xl="8" :lg="8" :md="12" :sm="24" :xs="24">
            <el-form-item label="Passport" prop="identity_card">
              <el-input type="input" v-model="form.identity_card" ></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :xl="8" :lg="8" :md="12" :sm="24" :xs="24">
            <el-form-item label="Marital" prop="marriage">
              <el-select v-model="form.marriage" placeholder="Please Select ">
                <el-option key="married" label="Married" value="married">
                </el-option>
                <el-option key="unmarried" label="UnMarried" value="unmarried">
                </el-option>
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :xl="8" :lg="8" :md="12" :sm="24" :xs="24">
            <el-form-item label="Education" prop="education">
              <el-select v-model="form.education" placeholder="Select Eduction">
                <el-option key="college" label="College" value="college">
                </el-option>
                <el-option key="highschool" label="Highschool" value="highschool">
                </el-option>
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :xl="8" :lg="8" :md="12" :sm="24" :xs="24">
            <el-form-item label="Address1" prop="address1">
              <el-input type="input" v-model="form.address1"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :xl="8" :lg="8" :md="12" :sm="24" :xs="24">
            <el-form-item label="Address2" prop="address2">
              <el-input type="input" v-model="form.address2"></el-input>
            </el-form-item>
          </el-col>
          <el-col :xl="8" :lg="8" :md="12" :sm="24" :xs="24">
            <el-form-item label="Telephone" prop="phone">
              <el-input type="input" v-model="form.phone"></el-input>
            </el-form-item>
          </el-col>
          <el-col :xl="8" :lg="8" :md="12" :sm="24" :xs="24">
            <el-form-item label="Phone" prop="mobile_phone">
              <el-input type="input" v-model="form.mobile_phone"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-card>
```
Because there are 5 cards, the picture only shows part of the content

![prototyping](https://github.com/LUJ13/images/blob/main/4.png?raw=true)

### <a name="ch3_4">IndexView.vue-Loan apply management</a>
Add a search function
```
<el-button type="primary" @click="queryName">Search</el-button>
```
![prototyping](https://github.com/LUJ13/images/blob/main/6.png?raw=true)

Displays different colors according to different states for user convenience.


```
<div v-if="column.property === 'status'">
    <el-tag :type="row[column.property] |    statusColor">{{
         row[column.property] | status
            }}
    </el-tag>
</div>

<el-button
              type="primary"
              @click="editApplication(row)"
              :disabled="[0, 2, 3, 6].indexOf(row['status']) === -1"
              >Edit</el-button
            >
            <el-button type="danger" @click="deleteApplication(row.id)"
              >Delete</el-button
            >
            <el-button
              type="success"
              @click="submitApplication(row.id)"
              :disabled="[0, 2, 3, 6].indexOf(row['status']) === -1"
              >Submit</el-button
```
![prototyping](https://github.com/LUJ13/images/blob/main/7.png?raw=true)
![prototyping](https://github.com/LUJ13/images/blob/main/8.png?raw=true)

## <a name="ref">Reference</a>
\[1]ElementUI design website-https://element.eleme.io/#/en-US/component/installation