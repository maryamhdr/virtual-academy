<div dir="rtl">
  
## جلسه چهارم - پیاده سازی ماشین حساب در Blazor
  
در این جلسه قصد داریم یک ماشین حساب ساده مطابق تصویر زیر با استفاده از Blazor پیاده سازی کنیم.

<img width="400px" src="images/img-1.png" />

همانند جلسه گذشته پروژه جدیدی به نام SimpleBlazorCalculator ایجاد کرده و مجددا فایل‌ها و پوشه‌های اضافی را مطابق جلسه گذشته حذف کنید. با این تفاوت که هر سه فایل موجود در پوشه Pages را حذف کنید.
  
داخل پوشه Pages  فایل جدید به نام Calculator.razor  ایجاد کنید.

  
وارد فایل Calculator.razor شده و در ابتدای این فایل کد زیر را برای تعیین مسیر این صفحه در مرورگر وارد کنید.

<div dir="ltr">

  ```razor
  
  @page "/calculator"
  
  ```
</div>

<img width="300px" src="images/img-2.png" />

 برای ایجاد ساختار اولیه ماشین حساب کد زیر را در فایل Calculator.razor  وارد کنید.

<div dir="ltr">

  ```html
  
    <div>
      <div>
          <div>
              <input type="text" placeholder="0"/>
          </div>
          <div>
              <input type="text" placeholder="0"/>
          </div>
          <div>
              <button>+</button>
              <button>-</button>
              <button>*</button>
              <button>/</button>
          </div>
          <div>
              <input type="text" placeholder="0" readonly/>
          </div>
      </div>
  </div>
  
  ```
</div>


از تگ های Input برای ایجاد کنترل‌های تعاملی برای فرم‌های تحت وب به منظور پذیرش داده‌ها از کاربر استفاده می‌شود. به دلیل گستردگی در انواع داده‌ها، انواع متفاوتی از تگ‌های input را داریم که نوع آنها را با استفاده ویژگی type این تگ، مانند موارد زیر مشخص می‌کنیم.


<div dir="ltr">

  ```html
  
  <input type="number">
  <input type="password">
  <input type="tel">
  <input type="text">(default value)
  <input type="url">
  
  ```
</div>
  
ویژگی placeholder در input می‌تواند شامل یک متن خیلی کوتاه باشد که اشاره به مقدار مورد انتظار یک المنت دارد.

در این تمرین همانطور که مشاهده می‌کنید ازدو تگ input برای گرفتن دو عدد از کاربر استفاده می‌کنیم.
و همچنین از یک تگ input با ویژگی readonly به معنای این که محتوای این تگ قابل تغییر نیست و فقط قابل خواندن است، برای نتیجه نهایی استفاده می‌کنیم.

  
<img width="300px" src="images/img-3.png" />

به منظور افزودن استایل به المنت در این جلسه، از نام class هر المنت، به عنوان selector استفاده می‌کنیم. در نتیجه کدهای مربوط به فایل Calculator.razor به صورت زیر تغییر می کنند.

<div dir="ltr">

  ```html
  
    <div class="container">
    <div class="card">
        <div class="field">
            <input type="text" placeholder="0"/>
        </div>
        <div class="field">
            <input type="text" placeholder="0"/>
        </div>
        <div class="action">
            <button class="btn">+</button>
            <button class="btn">-</button>
            <button class="btn">*</button>
            <button class="btn">/</button>
        </div>
        <div class="field result">
            <input type="text" placeholder="0" readonly/>
        </div>
    </div>
</div>
  
  ```
</div>

همان طور که در کد بالا می‌بینید ("class="field result) می‌توانیم مقادیر متعددی را برای ویژگی class هر المنت در نظر بگیریم. 
  
تفاوت استفاده از نام class به جای نام id در این است که اگر برای یک المنت id تعیین کنیم، از نام id آن المنت نمی‌توانیم برای المنت‌های دیگر استفاده کنیم. ولی همان طور که در کد بالا می‌بینید زمانی که از نام class برای انتخاب یک المنت استفاده می‌کنیم می توانیم از همان نام، برای المنت‌های دیگرهم، که می‌خواهیم همان پراپرتی‌ها را داشته باشند، استفاده کنیم.
زمانی که می‌خواهیم از نام class به عنوان selector استفاده کنیم، قبل از نام کلاس باید " . " اضافه کنیم.
با استفاده از کدهای زیر استایل مورد نظر ما ایجاد می‌شود.

<div dir="ltr">

  ```css
 .card {
    margin: 120px auto;
    padding: 20px;
    width: 400px;
    height: 400px;
    background-color: cornflowerblue;
    border-radius: 5px;
    box-shadow: 1px 2px 10px 0 rgba(0, 0, 0, 0.3);
}
 
.field {
    margin: 15px
}
 
input {
    padding: 10px;
    width: 350px;
    height: 30px;
    color: cornflowerblue;
    border: 2px solid #dcdcdc;
    text-align: center;
    font-size: 30px;
}
 
.result {
    margin-top: 75px;
}
 
.action {
    margin: 30px 0;
    text-align: center;
}
 
.btn {
    margin: 5px;
    width: 80px;
    height: 80px;
    border-radius: 5px;
    border: 2px solid #dcdcdc;
    line-height: 80px;
    color: cornflowerblue;
    font-size: 35px;
    cursor: pointer;
}
  
  ```
</div>

<img width="400px" src="images/img-4.png" />

فایل جدیدی به نام Calculator.razor.cs به منظور نوشتن متدها، برای چهار عمل اصلی (جمع، تفریق، ضرب، تقسیم) ایجاد می‌کنیم و کدهای زیر را وارد این فایل می‌کنیم.
  
<div dir="ltr">

  ```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;

namespace SimpleBlazorCalculator.Pages
{
    public partial class Calculator
    {
        public decimal Num1 { get; set; }

        public decimal Num2 { get; set; }

        public string Finalresult { get; set; }

        void AddNumbers()
        {
            Finalresult = (Num1 + Num2).ToString();
        }

        void SubtractNumbers()
        {
            Finalresult = (Num1 - Num2).ToString();
        }

        void MultiplyNumbers()
        {
            Finalresult = (Num1 * Num2).ToString();
        }

        void DivideNumbers()
        {
            if (Num2 != 0)
            {
                Finalresult = (Num1 / Num2).ToString("0.##");
            }
            else
            {
                Finalresult = "Cannot Divide by Zero";
            }
        }
    }
}



  ```
</div>

همانطور که در کد بالا می‌بینید داخل کلاس Calculator،  ازسه پارامتر استفاده می‌کنیم که Num1 و Num2  از نوع string بوده و قرار است دو عددی که از کاربر دریافت می‌کنیم را داخل خود نگه دارند و پارامتر finalresult  که از نوع decimal بوده و نتیجه نهایی را در خود نگه می‌دارد.

نوع decimal و یا دهدهی زمانی مناسب است که درجه دقت مورد نیاز، توسط تعداد ارقام سمت راست نقطه اعشاری تعیین شود. این اعداد معمولاً در برنامه های مالی ، برای مبالغ ارزی (به عنوان مثال ، 1.00 دلار) ، نرخ بهره (به عنوان مثال ، 2.625٪) و غیره استفاده می شود.

چهار متد هم به نام‌های AddNumbers، SubtractNumbers، MultiplyNumbers، DivideNumbers برای  چهار عمل اصلی داریم.

در داخل هر متد بعد از اعمال عملگر بر روی دو عدد، از متد ()ToStrin برای تبدیل نتیجه که به صورت decimal می‌باشد به string استفاده می کنیم و در نهایت داخل پارامتر Finalresult  قرار می‌دهیم.


برای نمایش اعشار تا دو رقم از ToString("0.##") استفاده می‌کنیم.

در متد DivideNumbers از یک شرط استفاده می کنیم چرا که در تقسیم اعداد، تقسیم یک عدد بر صفر تعریف نشده است. به همین منظور می‌توانیم با قرار دادن یک شرط، به این صورت که اگر عدد دوم مخالف صفر بود عمل تقسیم انجام و در غیر این صورت پیغام مناسب را به کاربر نمایش دهد، خروجی درست را به کاربر نمایش دهیم.
  
الگوی کلی دستورات شرطی if به صورت زیر ‌می‌باشد.
  
<img width="250px" src="images/img-5.png" />
  
  به منظور استفاده از ساختار شرطی از کلمه کلیدی if استفاده می‌کنیم. در داخل پرانتز شرط مورد نظر را نوشته، در صورت صحت شرط تعیین شده، مجموعه‌ای از دستورات در بلاک کد اول، اجرا و در غیر این صورت بعد از کلمه کلیدی else مجموعه دستورات در بلاک کد دوم، اجرا می‌شوند.

در مرحله بعد باید هر متد را بر روی رویداد onclick دکمه مربوطه فراخوانی کنیم. 
بدین ترتیب مجددا وارد فایل Calculator.razor شده و تغییرات زیر را بر روی کد اعمال می‌کنیم.

<div dir="ltr">

  ```html

  <div class="container">
    <div class="card">
        <div class="field">
            <input type="text" placeholder="0" />
        </div>

        <div class="field">
            <input type="text" placeholder="0" />
        </div>

        <div class="action">
            <button class="btn" @onclick="AddNumbers">+</button>
            <button class="btn" @onclick="SubtractNumbers">-</button>
            <button class="btn" @onclick="MultiplyNumbers">*</button>
            <button class="btn" @onclick="DivideNumbers">/</button>
        </div>

        <div class="field result">
            <input type="text" placeholder="0" readonly />
        </div>
    </div>
  </div>
  
  ```
</div>

با استفاده از ویژگی bind@ در ‌Blazor می‌توانیم مقادیر متغیرهای (num1, num2, finalresult) مربوط به هر input را به آنها نسبت دهیم. 
 
 در واقع ما یک اتصال داده بین متغیرها در کلاس calculator و این  input ها ایجاد می‌کنیم. بدین ترتیب زمانی که کاربر اعداد را وارد می‌کند، مقادیر داخل متغیرهای num1 و num2 نشسته و در مقابل مقدار متغیر finalresult را به input  سوم نسبت می‌دهیم و با هر تغییری در این متغیر مقدار input بروزرسانی می‌شود.

برای اعمال ویژگی bind@ کد را به صورت زیر تغییر دهید. 
 
<div dir="ltr">

  ```html

  <div class="container">
    <div class="card">
        <div class="field">
            <input type="text" placeholder="0" @bind="@Num1"/>
        </div>

        <div class="field">
            <input type="text" placeholder="0" @bind="@Num2"/>
        </div>

        <div class="action">
            <button class="btn" @onclick="AddNumbers">+</button>
            <button class="btn" @onclick="SubtractNumbers">-</button>
            <button class="btn" @onclick="MultiplyNumbers">*</button>
            <button class="btn" @onclick="DivideNumbers">/</button>
        </div>

        <div class="field result">
            <input type="text" placeholder="0" readonly @bind="@Finalresult" />
        </div>
    </div>
  </div>
  
  ```
</div>
 
  خروجی نهایی به صورت زیر می‌باشد.

  <img width="400px" src="images/calculator.gif" />

</div>