1.Form Validation
----------------html-----------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="form.css"> 
    <title>Registration Form</title>
</head>
<body>
    <h1>Registration Form</h1>
    <form id="registrationForm">
        <div>
            <label for="fullName">Full Name:</label>
            <input type="text" id="fullName" name="fullName" required>
            <span class="error" id="fullNameError"></span>
        </div>
        <div>
            <label for="email">Email Address:</label>
            <input type="email" id="email" name="email" required>
            <span class="error" id="emailError"></span>
        </div>
        <div>
            <label for="password">Password:</label>
            <input type="password" id="password" name="password" required>
            <span class="error" id="passwordError"></span>
        </div>
        <div>
            <label for="confirmPassword">Confirm Password:</label>
            <input type="password" id="confirmPassword" name="confirmPassword" required>
            <span class="error" id="confirmPasswordError"></span>
        </div>
        <div>
            <label for="dob">Date of Birth (YYYY-MM-DD):</label>
            <input type="text" id="dob" name="dob" required>
            <span class="error" id="dobError"></span>
        </div>
        <div>
            <button type="submit" id="submitButton" >Register</button>
        </div>
    </form>
    <script src="script.js"></script> 
</body>
</html>

-----------Javascript------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

function validateFullName() {
    const fullName = document.getElementById('fullName').value;
    const fullNameError = document.getElementById('fullNameError');
    const validName = /^[A-Za-z\s]{3,}$/.test(fullName);
    fullNameError.textContent = validName ? '' : 'Invalid name (min. 3 characters)';
    return validName;
}


function validateEmail() {
    const email = document.getElementById('email').value;
    const emailError = document.getElementById('emailError');
    const validEmail = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
    emailError.textContent = validEmail ? '' : 'Invalid email format';
    return validEmail;
}


function validatePassword() {
    const password = document.getElementById('password').value;
    const passwordError = document.getElementById('passwordError');
    const validPassword = /^(?=.*[A-Za-z])(?=.*\d).{8,}$/.test(password);
    passwordError.textContent = validPassword ? '' : 'Invalid password (min. 8 characters with letters, and numbers)';
    return validPassword;
}


function validatePasswordMatch() {
    const password = document.getElementById('password').value;
    const confirmPassword = document.getElementById('confirmPassword').value;
    const confirmPasswordError = document.getElementById('confirmPasswordError');
    const passwordMatch = password === confirmPassword;
    confirmPasswordError.textContent = passwordMatch ? '' : 'Passwords do not match';
    return passwordMatch;
}


function calculateAge() {
    const dob = document.getElementById('dob').value;
    const dobError = document.getElementById('dobError');
    const dobDate = new Date(dob);
    const currentDate = new Date();
    const age = currentDate.getFullYear() - dobDate.getFullYear();
    
    if (isNaN(age)) {
        dobError.textContent = 'Invalid date format (YYYY-MM-DD)';
        return false;
    }

    if (currentDate.getMonth() < dobDate.getMonth() || (currentDate.getMonth() === dobDate.getMonth() && currentDate.getDate() < dobDate.getDate())) {
        age--;
    }

    dobError.textContent = age >= 18 ? '' : 'You must be at least 18 years old';
    return age >= 18;
}


document.getElementById('fullName').addEventListener('input', validateFullName);
document.getElementById('email').addEventListener('input', validateEmail);
document.getElementById('password').addEventListener('input', validatePassword);
document.getElementById('confirmPassword').addEventListener('input', validatePasswordMatch);
document.getElementById('dob').addEventListener('input', calculateAge);

------------------------CSS--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
}

h1 {
    text-align: center;
}

form {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    background: #fff;
    border: 1px solid #ccc;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

div {
    margin-bottom: 15px;
}

label {
    font-weight: bold;
}

input[type="text"],
input[type="email"],
input[type="password"] {
    width: 100%;
    padding: 6px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

.error {
    color: red;
    font-size: 14px;
}


input:valid {
    border-color: green;
}


input:invalid {
    border-color: red;
}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
2.Working with API

----------------html-------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lab Exam Practice</title>
    <link rel="stylesheet" href="style.css">
    <script src="script.js"></script>
</head>
<body>

   <!-- ----------------------------------------------------- -->

    <div class="container-header">Random Joke</div>
    <div>API takes a few seconds to load data please wait</div>
    <button class="fetch-button" id="joke">New joke</button>
    <button class="fetch-button" id="clearjoke">Clear All Jokes</button>
    <!-- Jokes in A container -->
    <div class="items-container" id="jokes-container">
      
    </div>

   <!-- ----------------------------------------------------- -->

    <div class="container-header">Random Dog image</div>
    <div>API takes a few seconds to load data please wait</div>

    <button class="fetch-button" id="dog">New Dog</button>
    <button class="fetch-button" id="cleardog">Clear Dog Image</button>
    <!-- Random Dog image in A Container -->
    <div class="items-container" id="dog-container">

    </div>

    <!-- ---------------------------------------------------- -->

    <div class="container-header">Exchange Rates</div>
    <div>API takes a few seconds to load data please wait</div>

    <!-- Exchange Rates in A Container -->
    <button class="fetch-button" id="exchange">Get Exhange Rates</button>
    <button class="fetch-button" id="clearexchange">Clear Exchange Rates</button>
    <div class="items-container">
        <span>
        <div>Base</div>
        <select name="base" id="base">
            <option value="USD" selected>1 US Dollar</option>
            <option value="INR" >1 Indian Rupee</option>
            <option value="EUR" >1 Euro</option>
            <option value="AUD" >1 Australian Dollar</option>
            <option value="AED" >1 Dirham</option>

        </select>   
        </span>
        <table  id="exchange-container">
            <thead>
                <th>Country Code</th>
                <th>Exchange Rate</th>
            </thead>
            <tbody class="tbody" id="exchangebody">
                
            
            
            </tbody>
    
        </table>
    </div>

    <!-- ---------------------------------------------------- -->

    <div class="container-header">Book List</div>
    <div>API takes a few seconds to load data please wait</div>

    <!-- Books in A Container -->
    <button class="fetch-button" id="books">Get Books</button>
    <button class="fetch-button" id="clearbook">Clear Book List</button>
    <div class="items-container" id="books-container">
        <table  id="books-container">
            <thead>
                <th>Title</th>
                <th>Author Name</th>
                <th>Description</th>
                <th>Image</th>
            </thead>
            <tbody class="tbody" id="bookbody">
              
            
            </tbody>
    
        </table>

    
    </div>
    
    <!-- ---------------------------------------------------- -->
        
</body>
</html>

-------------------Javascript-------------------------------------------------
--------------------Jokes Api------------------------------
window.onload=()=>{
    //const jokesApi = "https://v2.jokeapi.dev/joke/Any"
    var jokeButton=document.getElementById("joke");
    var jokeClearButton=document.getElementById("clearjoke")

    jokeClearButton.addEventListener('click',()=>{
        document.getElementById("jokes-container").innerHTML=null
    })

    jokeButton.addEventListener('click',async()=>{
        console.log("joke button is pressed")
        await fetch(jokesApi).then((result)=>{
            result.json().then((data)=>{
                // console.log(data)
                var newJoke = document.createElement('div')
                newJoke.className = "single-item"
                if(data.type === "single"){
                    newJoke.innerHTML = data.joke
                }
                else if(data.type === "twopart"){
                    newJoke.innerHTML = `${data.setup} . ${data.delivery}`
                }

                if(data.flags.nsfw===true){
                    newJoke.style.border="2px solid red"
                    newJoke.style.backgroundColor="#ffb1b1"
                }

                document.getElementById("jokes-container").appendChild(newJoke)

            })
        }).catch((err)=>{
            console.log(err);
        })
    })


    // ------------------Dogs Api -----------------------------


    const dogApi="https://dog.ceo/api/breeds/image/random"
    var dogButton=document.getElementById("dog")
    var dogClearButton=document.getElementById("cleardog")

    
    dogClearButton.addEventListener('click',()=>{
        document.getElementById("dog-container").innerHTML=null
    })

    dogButton.addEventListener('click',async()=>{
        console.log("Dog button is pressed")
        await fetch(dogApi).then((res)=>{
            res.json().then((data)=>{
                // console.log(data)
                var newdog = document.createElement('img')
                newdog.className="item-image"
                newdog.src = data.message
                document.getElementById("dog-container").innerHTML=null
                document.getElementById("dog-container").appendChild(newdog)
            })

        }).catch((err)=>{
            console.log(err);
        })
    })

    // --------------------Exhange Rates Api-------------------------------


    
    // const exchangeApi = "https://api.apilayer.com/exchangerates_data/latest?base=USD"
    
    var myHeaders = new Headers()
    myHeaders.append("apikey","0h399deSlkFvh7EGq6XRKVJVoUIAbpoQ")

    var requestOptions = {
        method: 'GET',
        redirect: 'follow',
        headers: myHeaders
      };
    var exchangeButton=document.getElementById("exchange");
    var exchangeClearButton=document.getElementById("clearexchange")

    exchangeClearButton.addEventListener('click',()=>{
        document.getElementById("exchangebody").innerHTML=null
    })

    var exchangeRates={}
    exchangeButton.addEventListener('click',async()=>{
        exchangeRates={}
        document.getElementById("exchangebody").innerHTML=null
        console.log("Exchange button was clicked")
        var base = document.getElementById("base").value
        const exchangeApi = `https://api.apilayer.com/exchangerates_data/latest?base=${base}`
        await fetch(exchangeApi,requestOptions).then((res)=>{
            res.json().then((data)=>{
                // console.log(data);
                exchangeRates=data.rates
                // console.log(exchangeRates);
                for(const key in exchangeRates)
                {
                    var row = document.createElement("tr")
                    var countryCode = document.createElement("td")
                    countryCode.innerHTML=key
                    var rate= document.createElement("td")
                    rate.innerHTML=exchangeRates[key]
                    row.appendChild(countryCode)
                    row.appendChild(rate)
                    document.getElementById("exchangebody").appendChild(row)
                    // console.log(`${key} ---- ${exchangeRates[key]}`);
                }
            })

        }).catch((err)=>{
            console.log(err);
        })
    })

    // -------------Books API---------------------------

    const bookAPI = "https://api.nytimes.com/svc/books/v3/lists/2019-01-20/hardcover-fiction.json?api-key=QTd4H7HDVpLKhqIqtV42NmAthrt8ub4b"
    var bookButton = document.getElementById("books")
    var clearBookButton = document.getElementById("clearbook")

    clearBookButton.addEventListener('click',()=>{
        document.getElementById("bookbody").innerHTML=null
    })

    var bookList = []
    bookButton.addEventListener('click',async()=>{
        bookList = []
        console.log("Book Button Pressed");
        await fetch(bookAPI).then((res)=>{
            res.json().then((data)=>{
                bookList = data.results.books
                // console.log(bookList)
                for(let i = 0;i<bookList.length;i++){
                    var row = document.createElement("tr")
                    var title = document.createElement("td")
                    title.innerHTML = bookList[i].title
                    var author = document.createElement("td")
                    author.innerHTML = bookList[i].author
                    var desc = document.createElement("td")
                    desc.innerHTML = bookList[i].description
                    var bookimage = document.createElement("td")
                    var image = document.createElement('img')
                    image.src = bookList[i].book_image
                    image.width="100"
                    image.height="100"
                    bookimage.appendChild(image)
                    row.appendChild(title)
                    row.appendChild(author)
                    row.appendChild(desc)
                    row.appendChild(bookimage)
                    document.getElementById("bookbody").append(row)
                }
            })
        }).catch((err)=>{
            console.log(err);
        })

    })

}

------------------------CSS------------------------------------------------------
body{
    padding: 50px 100px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.button-container{
    display: flex;
    flex-direction: row;
    gap: 30px;
    align-items: center;
    margin: auto;

}

.fetch-button{
    padding: 8px 16px;
    font-size: 16px;
    font-weight: bold;
    color: #101010;
    border: 2px solid #101010;
    cursor: pointer;
    margin-bottom:30px ;
    /* border-radius: 3px; */
    box-shadow: 3px 3px 0px #101010;
}

.clear{
    padding: 5px 10px;
    background-color: black;
    color: white;
    margin: 5px 0px;
    cursor: pointer;
    font-weight: bold;
}

.fetch-button:hover{
    background-color: #101010;
    color: white;
    transition: 0.3s ease-in;
    box-shadow: 4px 4px 0px #939393;

}

.container-header{
    font-size: 30px ;
    font-weight: bold;
    text-align: left;
}
.items-container{
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin: auto auto 30px auto;
    padding: 20px;
    background-color: rgb(237, 237, 237);
    border-radius: 3px;
    justify-content: center;
    max-height: 500px;
    overflow-y: auto;
}

.items-container::-webkit-scrollbar{
    display: none;
}


.single-item{
    padding:10px;
    background-color: #e3e3e3;
    border-radius: 3px;
}

.single-item:hover{
    background-color: #d6d6d6;


}

.item-image{
    margin: auto;

}

table{
    width: 100%;
}

tbody{
    display:block;
    max-height:400px;
    overflow-y:auto;
    overflow-x: hidden;   
}

tbody::-webkit-scrollbar{
    display: none;    
}


thead , tr {
    display:table;
    width: 100%;
    table-layout:fixed;  
}
tbody,thead{
    width: 100%;
}



tr{
    padding: 5px; 
}


th{
    text-align: left;
    font-size: 16px;
    background-color: #232323;
    padding: 5px;
    /* border-radius: 8px; */
    color: white;
}

td{
    padding: 10px;
    /* border-radius: 8px; */
}

tr:hover td{
    background-color: lightgray;
    border-bottom:1px solid #101010;
    cursor: pointer;
}

input{
    padding: 10px;
    border: 2px solid #101010;
    /* border-radius: 5px; */
    flex:1;
    font-size: 16px;
}

select{
    padding: 5px;
}

-------------------------------JSON FETCH-------------------------------------
-------------------------------BOOKS.JSON-------------------------------------
[
    {
      "title": "Subtle art of not giving a F***",
      "author": "Mark Manson"
    
    },
    {
      "title": "How to win over friends and influence people",
      "author": "Dale Carnegie"
    
    }
   
  ]
  
  ----------------------------INDEX.HTML----------------------------------------
  <!DOCTYPE html>
<html>
<head>
<title>Fetch JSON Data with AJAX</title>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script>
function fetchBooks() {
  $.ajax({
    url: "books.json",
    dataType: "json",
    success: function(data) {
      displayBooks(data);
    }
  });
}

function displayBooks(data) {
  var bookList = document.getElementById("bookList");
  bookList.innerHTML = "";

  for (var i in data) {
    var book = data[i];
    var bookDiv = document.createElement("div");
    bookDiv.innerHTML = `
      <h3>${book.title}</h3>
      <p>${book.author}</p>
    
    `;
    bookList.appendChild(bookDiv);
  }
}

$(document).ready(function() {
  $("#fetchBooks").click(fetchBooks);
});
</script>
</head>
<body>
  <h1>Fetch JSON Data with AJAX</h1>
  <button id="fetchBooks">Fetch Books</button>
  <div id="bookList"></div>
</body>
</html>
---------------------------------------------XML VALIDATE--------------------------------------------
import xmlschema as xml

XML_SCHEMA = xml.XMLSchema(r"C:\Users\USER\OneDrive\Desktop\Ellam Padikk\MCA CHRIST\Webstack\employee\empschema.xsd")

if XML_SCHEMA.is_valid(r"C:\Users\USER\OneDrive\Desktop\Ellam Padikk\MCA CHRIST\Webstack\employee\emp.xml"):
    print("The xml is vaild")
else:
    print("Sorry, xml is not well formed or valid")
    
------------------------------------------XSL--------------------------------------------------------
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:template match="/">
    <html>
      <head>
        <title>Employee List</title>
      </head>
      <body>
        <h1>Employee List</h1>
        <table border="1">
          <tr>
            <th>Name</th>
            <th>Position</th>
            <th>Salary</th>
            <th>Phone Number</th>
            <th>Email</th>
          </tr>
          <xsl:for-each select="EMPLOYEES/EMPLOYEE">
            <tr>
              <td><xsl:value-of select="concat(personal_info/first_name,' ',personal_info/last_name)"/></td>
              <td><xsl:value-of select="employee_info/position"/></td>
              <td><xsl:value-of select="employee_info/salary"/></td>
              <td><xsl:value-of select="contact_info/contact_number"/></td>
              <td><xsl:value-of select="contact_info/email"/></td>
            </tr>
          </xsl:for-each>
        </table>
      </body>
    </html>
  </xsl:template>
</xsl:stylesheet>
