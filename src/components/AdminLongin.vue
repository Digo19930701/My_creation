<template>
  
    <div class="login" >
        
        <div class="admin">商家登入</div>
        <el-form :model="loginForm" class="loginForm"  >
          <el-form-item label="帳號" :label-width="formLabelWidth" >
            <el-input v-model="loginForm.account" autocomplete="off" style="height: 50px; width: 500px;"/>
          </el-form-item>
          <el-form-item label="密碼" :label-width="formLabelWidth">
            <el-input v-model="loginForm.password" autocomplete="off" style="height: 50px; width: 500px;"/>
          </el-form-item>
          <div style="margin-left: 120px;">
            <el-button  @click="response" style="width: 200px; height: 50px;">登入</el-button>
            <el-button @click="dialogFormVisible = true" style="width: 200px; height: 50px;">註冊</el-button>           
            <el-link @click="verifyEmail =true" style="color: red; margin-left: 20px;">忘記密碼</el-link>
        </div>
        </el-form>
      
      
        <div style="margin-top: 50px; ">
          <img src="./config/image/googleLogin.png" >
        </div>
  
        
    
  
  
    
    
        
    
        <el-dialog v-model="dialogFormVisible" title="商家註冊">
          <el-form :model="register">
            <el-form-item  :label-width="formLabelWidth">
            <el-input v-model="register.mail" label-width="100px" autocomplete="off" type="register" placeholder="請輸入信箱" id="registerEamil"/>
            </el-form-item>
            <el-form-item  :label-width="formLabelWidth">
            <el-input v-model="register.Password" label-width="100px" autocomplete="off" type="register" placeholder="請輸入密碼" show-password/>
            </el-form-item>
            <el-form-item  :label-width="formLabelWidth">
            <el-input v-model="register.uniformNumbers" label-width="100px" autocomplete="off" type="register" placeholder="統一編號" show-password/>
            </el-form-item>
            <div><GoogleReCaptchaV2 /></div>
            
            <label for="option1">
              <input type="checkbox" id="option1" name="option"><el-link @click="read=true">已閱讀註冊相關資訊</el-link> 
          </label><br>
          </el-form>
          
          <!-- <el-checkbox v-model="checkbox" style="margin-left:70%;" type="checkbox" id="checkbox" name="checkbox" >我不是機器人</el-checkbox> -->
          <!-- <input type="checkbox" id="checkbox" v-model="checkbox">
            <label for="checkbox"></label> -->
          <template #footer>
            <span class="dialog-footer">
              
              
              <el-button type="primary" @click="submitForm ">註冊</el-button>
              <el-button @click="dialogFormVisible = false">取消</el-button>
            </span>
          </template>
        </el-dialog>
  
        <el-dialog v-model="verifyEmail" title="輸入信箱">
          <el-form :model="verifyemail">
            <el-form-item  :label-width="formLabelWidth">
            <el-input v-model="verifyemail.mail" label-width="100px" autocomplete="off" type="forgetPs" placeholder="請輸入信箱" />
            </el-form-item>
          </el-form>
          
          <template #footer>
            <span class="dialog-footer">
              <el-button type="primary" @click="forgetPassword = true" > 下一步</el-button>
              <el-button @click="verifyEmail = false">取消</el-button>
            </span>
          </template>
        </el-dialog>
  
        <el-dialog v-model="forgetPassword" title="忘記密碼">
          <el-form :model="forgetPs">
            
            <el-form-item  :label-width="formLabelWidth">
            <el-input v-model="forgetPs.verifypassword" label-width="100px" autocomplete="off" type="forgetPs" placeholder="請輸入驗證碼" />
            </el-form-item>
            
            <el-form-item  :label-width="formLabelWidth">
            <el-input v-model="forgetPs.newpassword" label-width="100px" autocomplete="off" type="forgetPs" placeholder="輸入新密碼" show-password/>
            </el-form-item>
          </el-form>
          
          <template #footer>
            <span class="dialog-footer">
              <el-button type="primary" @click="registerout"> 送出</el-button>
              <el-button @click="forgetPassword = false">取消</el-button>
            </span>
          </template>
        </el-dialog>

        <el-dialog v-model="read">
                    <div>1. 認知與接受條款
                    「本網站」係依據本服務條款提供本網站旗下所有聯盟服務 (以下簡稱「本服務」)。當您使用本網站時，即表示您已閱讀、瞭解並同意接受本約定書之所有內容。本網站有權於任何時間修改或變更本約定書之內容，建議您隨時注意該等修改或變更。您於任何修改或變更後繼續使用本網站，視為您已閱讀、瞭解並同意接受該等修改或變更。如果您不同意本約定書的內容，或者您所屬的國家或地域排除本約定書內容之全部或一部時，您應立即停止使用本網站。
                    若您為未滿十八歲，除應符合上述規定外，並應於您的家長（或監護人）閱讀、瞭解並同意本約定書之所有內容及其後修改變更後，方得使用或繼續使用本網站。當您使用或繼續使用本網站時，即表示您的家長（或監護人）已閱讀、瞭解並同意接受本約定書之所有內容及其後修改變更。
                    </div> 
                    <div>
                    2. 您的註冊義務

                    為了能使用本服務，您同意以下事項：
                    (a) 依本服務註冊表之提示提供您本人正確、最新及完整的資料，
                    (b) 維持並更新您個人資料，確保其為正確、最新及完整。若您提供任何錯誤或不實的資料，本網站有權暫停或終止您的帳號，並拒絕您使用本服務之全部或一部。
                    (c) 不論您是否註冊成會員，您同意完全遵守本同意書任何規範條款。

                    </div>

                    <div>
                    3. 本網站隱私權政策
                    關於您的會員註冊以及其他特定資料依本公司「隱私權政策」受到保護與規範。您在本站聊天室之聊天或言論，同意遵循本站遊戲規則，站長及管理人員有權監看所有聊天內容，絕無異議。
                    </div>
                    <div>
                        4. 會員帳號、密碼及安全
                    完成本服務的登記程序之後，您將收到一個密碼及帳號。維持密碼及帳號的機密安全，是您的責任。利用該密碼及帳號所進行的一切行動，您將負完全的責任。您並同意以下事項：(a)您的密碼或帳號遭到盜用或有其他任何安全問題發生時，您將立即通知本網站，且(b)每次連線完畢，均結束您的帳號使用。
                    </div>
                    
                    <div>
                        5. 兒童及青少年之保護
                    兒童及青少年上網已經成為無可避免之趨勢，使用網際網路獲取知識更可以培養子女的成熟度與競爭能力。然而網路上的確存有不適宜兒童及青少年接受的訊息，例如色情與暴力的訊息，兒童及青少年有可能因此受到心靈與肉體上的傷害。因此，為確保兒童及青少年使用網路的安全，並避免隱私權受到侵犯，家長（或監護人）應盡到下列義務：
                    a.先檢閱各該網站是否有保護個人資料的隱私權政策，再決定是否同意提出相關的個人資料；並應持續叮嚀兒童及青少年不可洩漏自己或家人的任何資料（包括姓名、地址、電話、電子郵件信箱、照片、信用卡號等）給任何人。也不可以單獨接受網友的邀請或贈送禮物而與之見面。
                    b.謹慎選擇合適網站供兒童及青少年瀏覽。未滿十二歲之兒童上網時，應全程在旁陪伴，十二歲以上未滿十八歲之青少年上網前亦應斟酌是否給予同意。
                    </div>
                    <div>
                        6. 使用者的守法義務及承諾

                    您充分了解並同意完全，遵循本站各項規則條款，如因言行不當被懲處，絕無異議。如屬被誤踢或因IP接近被踢者而被鎖，請告知站長解除。此一狀況屬聊天遊戲之常態，本站恕不負擔任何賠償責任。

                    您承諾絕不為任何非法目的或以任何非法方式使用本網站，並承諾遵守中華民國相關法規及一切使用網際網路之國際慣例。您若係中華民國以外之使用者，並同意遵守所屬國家或地域之法令。您同意並保證不得利用本服務從事侵害他人權益或違法之行為，包括但不限於：
                    A. 公布或傳送任何誹謗、侮辱、具威脅性、攻擊性、不雅、猥褻、不實、違反公共秩序或善良風俗或其他不法之文字、圖片或任何形式的檔案於本網站；
                    B. 侵害他人名譽、隱私權、營業秘密、商標權、著作權、專利權、其他智慧財產權及其他權利；
                    C. 違反依法律或契約所應負之保密義務；
                    D. 冒用他人名義使用本服務；
                    E. 傳輸或散佈電腦病毒；
                    F. 從事不法交易行為或張貼虛假不實、引人犯罪之訊息；
                    G. 販賣槍枝、毒品、禁藥、盜版軟體或其他違禁物；
                    H. 提供賭博資訊或以任何方式引誘他人參與賭博；
                    I. 濫發廣告郵件或廣告留言等；
                    J. 其他本網站有正當理由認為不適當之行為。

                    </div>
                    

                    
        </el-dialog>
  
        
      </div>
  
     
    </template>
    
    <script lang="ts" setup>
    
    import { dataType } from 'element-plus/es/components/table-v2/src/common';
    import { reactive, ref } from 'vue'
    import GoogleReCaptchaV2 from './GoogleReCaptchaV2.vue'
    import axios from 'axios';
    
    
    
    
    
    const dialogFormVisible = ref(false)
    const read = ref(false)
    const verifyEmail = ref(false)
    const forgetPassword = ref(false)
    const checkbox = ref(false);
    const formLabelWidth = '100px'
    
    const register = reactive({
    mail: '',
    Password: '',
    uniformNumbers:'',
    
    
  })
    
    const forgetPs = reactive({
      verifypassword:'',
      newpassword:'',
  
    })
    const verifyemail=reactive({
      mail: '',
     
  
    })
    
    const loginForm = reactive({
      account: '',
      password: ''
  
    })
  
    const response = () => {
      const account = loginForm.account;
      const password = loginForm.password;
    
            console.log('account=' + account + '******' + 'password=' + password);
            // window.location.href = 'http://localhost:8080/api/login',{ account: account, password: password };
            
            const user = {
            Account: account,
            Password: password
          };
  
          axios.post("http://127.0.0.1:8080/api/login",  user, {
            headers: {
              'Content-Type': 'application/json'
            }
          })
          .then(response => { 
            console.log(response.data);
          })
          .catch(error => {
            
            console.error(error);
          });
  
  };
  
  
  
  
    const login = () => { 
      console.log("loginForm",loginForm)
    }
    const registerout = () => { 
      
      console.log("register",register)
    }
    
    
    function submitForm() {
      
      // console.log('in')
      var option1 = document.getElementById("option1");
  
  
      if (option1.checked) {
                  alert("已勾選");
       
              } else {
                  alert("請勾選註冊相關資訊");
      }
  
              
  
  
          // const ariaCheckedValue = checkboxElement.getAttribute('aria-checked');
          // console.log('aria-checked 属性的值:', ariaCheckedValue);
          // if (aria-checked == false) {
          //   const ariaCheckedValue = checkboxElement.getAttribute('aria-checked');
          // }else{
          //     alert('表單已提交');
          // }
  
          
      }
   
  
      const sendPostRequest = async () => {
      window.location.href = 'http://localhost:8080/ecpayCheckout';
      // axios.post('http://localhost:8080/ecpayCheckout', {})
      //     .then(response => {
      //         responseHTML.value = response.data
      //         document.getElementById('ECpayt').innerHTML = responseHTML.value;
      //         console.log(responseHTML.value)
      //     })
      //     .catch(error => {
      //         console.log(error)
      //     })
  };
    
    </script>
    
    
    
    <style scoped>
    .login {
      background-color: #f8d479;
      text-align: center;
      height: 100vh;
      display: block; /*顯示  彈性盒子佈局  */
      align-items: center;
      justify-content: center;
      background-image: url(".//config/image/logoicon.png");
      background-size: 100% 100%;
    }
    
    .loginForm {
      display: inline-block;
      vertical-align: middle;
      text-align: center;
      margin-right:5%;
    }
    
    .dialog-footer button:first-child {
      margin-right: 10px;
    
    }
    .admin{
        font-size: 50px;
        
    }
    
   
    
    </style>
    