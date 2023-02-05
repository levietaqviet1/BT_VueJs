# :notebook_with_decorative_cover: Table of Contents
- [Cài đặt môi trường](#Cài-đặt-môi-trường)

## Cài đặt môi trường

- `visual studio code`

![image](https://user-images.githubusercontent.com/85175337/216076021-f15ecc9d-75a3-4b02-a00e-e8b6b7f40102.png)

Trong visual studio code viết tắt VS code vào Extensions cài Live Server

Ảnh cần cài trong VS code:

![image](https://user-images.githubusercontent.com/85175337/216078156-d3644ef7-3e66-45ca-827f-81a27046cb4d.png)

Sau khi cài xong chuột phải vào trong html sẽ hiện Open with Live Server bấm vào để thấy phép màu:

![image](https://user-images.githubusercontent.com/85175337/216078758-a96b531e-ca85-4aab-9b76-49d92113a09c.png)

- `nodejs`

![image](https://user-images.githubusercontent.com/85175337/216075867-108a182f-9701-4268-9a3f-ee4330e1da99.png)


+ Trước khi cài `nodejs` có thể kiểm tra xem máy cài chưa ở `CMD` trong máy gôm 2 câu lệch: 
`node -v` nếu có nó sẽ hiện phiên bản nếu không sẽ báo ko có
`npm` nếu có nó sẽ hiện thông tin còn không thì ngược lại 

Ảnh minh họa khi đã cài thành công:

![image](https://user-images.githubusercontent.com/85175337/216075580-efdc506a-38db-4215-8a66-0ef2408dfa04.png)

- Git 

![image](https://user-images.githubusercontent.com/85175337/216076428-e83490f6-39ab-458d-bbc1-383c77160a46.png)

+ Kiểm tra đã cài đặt hay chưa thì chuột phải chắc chắn nhất là chuột phải ở trong thư mục máy xem hiện giống ảnh ko:

![image](https://user-images.githubusercontent.com/85175337/216076563-01b45f66-a80d-4066-8818-d35579f6e54d.png)

 ## Basic Vue in scrip

scrip để chạy đc

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
```

```vue
<script>
  var vueInstance = new Vue({
    el: '#app',
    data: {
      title: '2. chay thu'
    },
    methods: {
      say: function(text){
        return 'Hello' + text;
      }
    }
  });
  // hệ thống phản ứng. Reactivity
  console.log(vueInstance);

  setTimeout(()=> {
    vueInstance.title = " 2. chay thu 1.2";
  },2000)
</script>
```

Kết hợp với Html cao hơn:

```html
<body>
    <div id="app">
        {{title}} <a v-bind:href="URL" v-bind:target="tar">{{hien}}</a>
        <p>{{testHTML}} </p><!-- ko dc -->
        <p>{{checkDieuKien?'dc':'ko'}}</p><!-- dùng so sánh kiểu này đc-->
        <p>{{formatPrice()}}</p>
	<h1>{{count}}</h1>
        <button v-on:click="handleClick">click1</button> <!-- dùng v-on: kết hợp với event  -->
        <button v-on:click="count += 2">click2</button> <!-- có thể trực tiếp viết vào -->
    </div>

</body>
```

```vue
<script>
    // intl.numberformat
    const number = 123456.789; 
    console.log(new Intl.NumberFormat('de-DE', { style: 'currency', currency: 'EUR' }).format(number));
    // Expected output: "123.456,79 €"

    var vueInstance = new Vue({
        el: '#app',
        data: {
            title: 'Link nè: '
            // đối với url,tar để sử dụng đc thì cần thêm v-bind: ở htlm và ko cần {{}}
            , URL: 'https://www.youtube.com/watch?v=AHPkqa5ZaN0&list=PLv6GftO355AtDjStqeyXvhA1oRLuhvJWf&index=6'
            , tar: '_blank'
            , hien: 'nhấn'
            , testHTML: '<h1>ok</h1>'
            , checkDieuKien: false
            , price: 10000
            , count: 0

        },
        methods: {
            formatPrice() {
                return new Intl.NumberFormat('de-DE', { style: 'currency', currency: 'VND' }).format(this.price)
            }
            , handleClick() {
                this.count++;
            }
        }
    });
</script>
```

Kết hợp với Html với login basic:

```html 
<body>
    <div id="app">
        <!-- v-on:submit.prevent nằm trong Event Handling của Vue.js 
        Chức năng nó xử lý giống e.preventDefault()
        v-on:mousemove.stop giống e.stopPropagation();
        -->
        <form action="./serve" v-on:submit.prevent="handleSubmitForm"> 
            <label for="fN">Input First Name</label>
            <input id="fN" type="text" name="fName"><br><br>
            <label for="email">Input Email</label>
            <input id="email" type="text" name="email"><br><br>
            <input type="submit" value="Dang nhap">
        </form>
    </div>
</body>
```

```vue
<script>
    var vueInstance = new Vue({
        el: '#app',
        data: {
            title: '2. chay thu'
        },
        methods: {
            handleSubmitForm(e) {
                console.log(e);
                // e.preventDefault() // dùng để ngăn ko cho chuyển trang ( chuyến action hay là server) 
                // e.stopPropagation(); // dùng để chỉ chạy ko liên quan đến thẻ cha
            }
        }
    }); 
</script>
```

Sự khác biệt giữa Computed và Methods:

+ Computed  tuy khai báo giống như 1 hàm tuy nhiên nó sẽ được lưu vào trong đối tượng Vue 

+ Hàm trong Computed chỉ được thực thi khi mà có bất kỳ dữ liệu nào trong hàm có sự thay đổi 

+ Trong Methods thì chạy hết dễ gây lãng phí nếu có nhiều hàm nên tránh viết tính toán dữ liệu data 


```html 
<body>
    <div id="app">
        <p>{{messs}}</p>
        <p>{{reversedMessage}}</p>  <!-- Khi gọi tới thì ko cần () :)  -->
    </div>
</body>
<script>
  var vueInstance = new Vue({
    el: '#app',
    data: {
       messs: 'hello'
    },
    computed: {
        reversedMessage(){
            return this.messs.split('').reverse().join('')
        }
    }
  }); 
</script>
```

B6 Ràng buộc dữ liệu 2 chiều

```html 
<body>
    <!-- v model -->
    <div id="app">
        <p>{{fName}}</p>
        <!-- Khi load lên thì input có value = fName 
            và khi value input thay đổi thì thẻ <p>{{fName}}</p> cũng đổi theo
             => Ràng buộc dữ liệu 2 chiều -->
        <input v-model="fName" type="text" placeholder="Nhap first name"> 
        <!-- <input v-on:keyup="handleKeyUp" type="text" placeholder="Nhap first name"> -->
    </div>
</body>
<script>
    var vueInstance = new Vue({
        el: '#app',
        data: {
            fName: 'hello'
        },
        methods: {
            // handleKeyUp(e) {
            //     //console.log(e.target.value);
            //     this.fName = e.target.value;
            // }
        }
    }); 
</script>
```

B7 Ràng buộc Class bằng VueJs

+ Sử dụng v-bind để ràng buộc class

```html 
<body>
    <!-- Có thể xem thêm cứ pháp Object Syntax -->
    <!-- https://vuejs.org/guide/essentials/class-and-style.html#binding-html-classes  -->
    <div id="app">
        <div v-bind:class="'demo_' + textClass"> </div>
        <div class="demo2" v-bind:class="objClass"></div>
        
    </div>
</body>
<script>
    var vueInstance = new Vue({
        el: '#app',
        data: {
            textClass: 'active',
            isActive: true,
            isError: false
        },
        computed: {
            objClass() {
                return {
                    active: this.isActive,
                    error: this.isError
                }
            }
        }
    }); 
</script>
```
![image](https://user-images.githubusercontent.com/85175337/216807497-23e5dc5d-17ba-4e33-95e1-db8ea3fd610b.png)

B8 Ràng Buộc Style cho phần tử

```html
<body> 
    <div id="app">
        <!-- Lưu ý: 
        Trong javascrip với css font-size trong js chuyển thành fontSize  
        Viết hoa chữ cái đầu sau dấu gạch và xóa khoảng trắng cách-->
        <div class="demo" v-bind:style="objectStyle">
            <div class="demoB8" v-bind:style="{color: activeColor, fontSize: fontSize+'px'}" >VueJs</div>
        </div> 
    </div>
</body>
<script>
    var vueInstance = new Vue({
        el: '#app',
        data: {
            activeColor: 'red',
            fontSize: '30',
            backGroup: 'https://i.pinimg.com/280x280_RS/72/64/0f/72640fdec1bc3437e801808e225bc8c4.jpg'
        },
        computed: {
          background(){
            return 'url('+this.backGroup+')';
          },
          objectStyle(){
            return 
            {
                backgroundImage: this.background // gọi lại có thể dùng dễ hơn
            }
          }
        }
    }); 
</script>
```