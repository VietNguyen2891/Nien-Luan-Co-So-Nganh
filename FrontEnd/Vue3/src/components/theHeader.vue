<template>
  <!-- <head>
    <link rel="icon" href="../assets/banner_home/p1.png">
  </head> -->
  <!-- <div class="top-bar w-1200">
        <div class="container">
            <div class="row">
              <div class="header-meta-list">
                <div><a href="/">150 Cua hang khap ca nuoc</a></div>
              </div>
            </div>
        </div>
    </div> -->
  <!-- <link rel="icon" href="./src/assets/banner_home/logo.png"> -->

  <div class="header">
    <nav id="navbar" class="navbar fixed-top navbar-expand-lg navbar-light">
      <div class="container">
        <a
          class="navbar-brand"
          href="#"
          style="padding-left: 10px; padding-top: 10px"
          ><h3>King Coffee</h3></a
        >
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div
          class="collapse navbar-collapse justify-content-end align-center navbar-light"
          id="navbarNav"
        >
          <ul class="navbar-nav ml-auto">
            <router-link to="/" style="text-decoration: none !important">
              <li class="nav-item active">
                <a class="nav-link" href="" style="color: black">Trang Chủ</a>
              </li>
            </router-link>
            <li
              class="nav-item dropdown"
              @mouseover="isMenuHovered = true"
              @mouseleave="isMenuHovered = false"
            >
              <a
                class="nav-link dropdown-toggle"
                href="#"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
                style="color: black"
              >
                Menu
              </a>
              <ul
                class="dropdown-menu"
                :class="{ show: isMenuHovered }"
                style="background-color: rgba(255, 255, 255, 0.8)"
              >
                <router-link
                  to="/collections/AllCollections"
                  style="text-decoration: none !important"
                >
                  <li>
                    <a class="dropdown-item" href="" style="color: black"
                      >Tất Cả</a
                    >
                  </li>
                </router-link>
                <router-link
                  to="/collections/Coffee"
                  style="text-decoration: none !important"
                >
                  <li>
                    <a class="dropdown-item" href="" style="color: black"
                      >Cà Phê</a
                    >
                  </li>
                </router-link>
                <router-link
                  to="/collections/Tea"
                  style="text-decoration: none !important"
                >
                  <li>
                    <a class="dropdown-item" href="" style="color: black"
                      >Trà</a
                    >
                  </li>
                </router-link>
                <router-link
                  to="/collections/MilkTea"
                  style="text-decoration: none !important"
                >
                  <li>
                    <a class="dropdown-item" href="" style="color: black"
                      >Trà Sữa</a
                    >
                  </li>
                </router-link>
                <router-link
                  to="/collections/Frosty"
                  style="text-decoration: none !important"
                >
                  <li>
                    <a class="dropdown-item" href="" style="color: black"
                      >Đá Xay</a
                    >
                  </li>
                </router-link>
              </ul>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" style="color: black">Dịch Vụ</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" style="color: black">Cửa Hàng</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" style="color: black">Liên Hệ</a>
            </li>
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                v-if="this.userId"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
                style="color: black"
              >
                <!-- {{ this.userId }} -->
                {{ this.user.username }}
              </a>
              <a
                class="nav-link dropdown-toggle"
                href="#"
                v-if="!this.userId"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
                style="color: black"
              >
                Tài khoản
              </a>
              <ul
                class="dropdown-menu"
                style="background-color: rgba(255, 255, 255, 0.8)"
              >
                <router-link
                  to="/login"
                  style="text-decoration: none !important"
                >
                  <li>
                    <a
                      class="dropdown-item"
                      v-if="!this.userId"
                      href="#"
                      style="color: black"
                      >Đăng Nhập</a
                    >
                  </li>
                  <li>
                    <a
                      class="dropdown-item"
                      v-if="!this.userId"
                      href="#"
                      style="color: black"
                      >Đăng ký</a
                    >
                  </li>
                </router-link>
                <router-link to="/" style="text-decoration: none !important">
                  <li @click="loginpage()">
                    <a
                      class="dropdown-item"
                      v-if="this.userId"
                      style="color: black"
                      >Thoát</a
                    >
                  </li>
                </router-link>
              </ul>
            </li>
          </ul>
        </div>
      </div>
      <router-link
        to="/offerProduct/cart"
        style="text-decoration: none !important"
      >
        <div class="cart-button" style="margin-right: 10px">
          <span class="cart-icon">
            <i class="fas fa-shopping-cart"></i>
          </span>
          <span class="cart-label">Cart {{ cartQuantity }}</span>
          <!-- <span class="cart-items" @click="shoppingPage()">{{ cartQuantity }}</span> -->
        </div>
      </router-link>
      <!-- <div class="microphone-icon">
        <span class="microphone">
          <i class="fas fa-microphone"></i>
          <span class="recording-icon"></span>
        </span>
      </div> -->
    </nav>
  </div>
</template>

<script>
import axios from "../services/axios";
export default {
  props: ["cartQuantity"],
  name: "MyPage",
  data() {
    return {
      userId: "",
      user: {},
      isMenuHovered: false,
    };
  },
  methods: {
    loginpage() {
      localStorage.removeItem("userId");
      // document.location.href = "/";
      this.userId = "";
    },
  },
  created() {
    // Fetch and set the token from localStorage
    this.userId = localStorage.getItem("userId");

    axios.get(`/admin`).then((res) => {
      // console.log(res.data);
      this.user = res.data.find((user) => user.phone == this.userId);
    });
  },
};


// Tro ly ao
// var SpeechRecognition = SpeechRecognition || webkitSpeechRecognition;

// const recognition = new SpeechRecognition();
// const synth = window.speechSynthesis;
// recognition.lang = 'vi-VI';
// recognition.continuous = false;

// const microphone = document.querySelector('.microphone');

// const speak = (text) => {
//     if (synth.speaking) {
//         console.error('Busy. Speaking...');
//         return;
//     }

//     const utter = new SpeechSynthesisUtterance(text);

//     utter.onend = () => {
//         console.log('SpeechSynthesisUtterance.onend');
//     }
//     utter.onerror = (err) => {
//         console.error('SpeechSynthesisUtterance.onerror', err);
//     }

//     synth.speak(utter);
// };

// const handleVoice = (text) => {
//     console.log('text', text);

//     // "thời tiết tại Đà Nẵng" => ["thời tiết tại", "Đà Nẵng"]
//     const handledText = text.toLowerCase();
//     if (handledText.includes('thời tiết tại')) {
//         // const location = handledText.split('tại')[1].trim();
//         // console.log('location', location);
//         // searchInput.value = location;
//         // const changeEvent = new Event('change');
//         // searchInput.dispatchEvent(changeEvent);
//         console.log("Ha noi");
//         return;
//     }

//     const container = document.querySelector('.container');
//     if (handledText.includes('thay đổi màu nền')) {
//         // const color = handledText.split('màu nền')[1].trim();
//         // container.style.background = color;
//         console.log("mau do");
//         return;
//     }

//     if (handledText.includes('màu nền mặc định')) {
//         // container.style.background = '';
//         console.log("mau mac dinh");
//         return;
//     }

//     if (handledText.includes('mấy giờ')) {
//         // const textToSpeech = `${moment().hours()} hours ${moment().minutes()} minutes`;
//         // speak(textToSpeech);
//         console.log("2 gio r");
//         return;
//     }

//     speak('Try again');
// }

// microphone.addEventListener('click', (e) => {
//     e.preventDefault();

//     recognition.start();
//     microphone.classList.add('recording');
// });

// recognition.onspeechend = () => {
//     recognition.stop();
//     microphone.classList.remove('recording');
// }

// recognition.onerror = (err) => {
//     console.error(err);
//     microphone.classList.remove('recording');
// }

// recognition.onresult = (e) => {
//     console.log('onresult', e);
//     const text = e.results[0][0].transcript;
//     handleVoice(text);
// }
</script>

<style>
#header {
  background-color: rgba(255, 255, 255, 0.8);
  /* box-sizing: border-box;
  border-bottom: black; */
}

/* #navbarNav{
    background-color: rgba(255, 255, 255, 0.8);
  } */
#navbar {
  background-color: rgba(255, 255, 255, 0.8);
  border-bottom: 1px solid #00000026;
}

.dropdown-menu {
  background-color: rgba(255, 255, 255, 0.8);
}

.nav-item .nav-link {
  color: rgba(0, 0, 0, 0.9);
}

.nav-item .dropdown {
  color: rgba(0, 0, 0, 0.9);
}

a .nav-link .dropdown-toggle {
  color: rgba(0, 0, 0, 0.9);
  background-color: rgba(255, 255, 255, 0.8);
}

#a {
  color: rgba(0, 0, 0, 0.9);
}

.container {
  width: 960px;
  margin-right: auto;
  margin-left: auto;
  padding-left: 15px;
  padding-right: 15px;
}

.cart-button {
  background-color: #ff5722;
  color: #fff;
  display: inline-block;
  padding: 7px 14px;
  border-radius: 50px;
  cursor: pointer;

  /* transition: background-color 0.3s ease-in-out; */
  /* position: fixed;
  bottom: 60px; 
  right: 60px;  */
}

.cart-button:hover {
  background-color: #e64a19; /* Slightly darker shade on hover */
}

.cart-icon {
  font-size: 24px;
  vertical-align: middle;
  margin-right: 10px;
}

.cart-label {
  font-weight: bold;
  font-size: 16px;
  vertical-align: middle;
  margin-right: 5px;
}

.cart-items {
  background-color: #e64a19;
  color: #fff;
  border-radius: 50%;
  padding: 5px 10px;
  font-weight: bold;
  /* margin-top: 120px; */
}

.nav-item {
  margin-left: 20px;
}

/* .microphone-icon {
  position: absolute;
  top: 70px;
  right: 20px; 

}

.microphone{
  margin-top: 20px;
  size: 40px;

}

.microphone {
    cursor: pointer;
}

.microphone .recording-icon {
    display: none;
    width: 10px;
    height: 10px;
    background-color: #e22d2d;
    border-radius: 50%;
    animation: pulse 1.5s infinite linear;
}

.microphone.recording .recording-icon {
    display: inline-block;
}

.microphone.recording .fa-microphone {
    display: none;
} */
</style>
