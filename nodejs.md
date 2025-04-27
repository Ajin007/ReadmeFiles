## CRUD Project:

  ```
      class Notetaking {
        constructor(){
            this.notes=[];
            this.currentId=1;
        }
    
        // addNote
        addNote(title,content){
           let note={
                id : this.currentId++,
                title,
                content 
            }
    
            // this.notes.push(note);
        this.notes=[...this.notes,note];
           
        console.log(`Note added:${JSON.stringify(note)}`);
        console.log(`Note added:${JSON.stringify(this.notes)}`);
        
            return note;
        }
    
        // this is updateNote with the find
        updateNote(id,updates){
           let updatedValue= this.notes.find((notes)=>notes.id === id)
           if(updatedValue){
            Object.assign(updatedValue,updates);
            console.log("this is the updated data",updatedValue);
            console.log(this.notes);
    return updatedValue;        
           }else{
            console.log("There is no value to update");
            return undefined;
           }       
        }
        //now to update the note with the findall
        updateNotewithFindINdex(id,updates){
         let updatedIndex=this.notes.findIndex((note)=>note.id === id);
    
         if(updatedIndex){
    
            const updatedData={...this.notes[updatedIndex],...updates};
            this.notes=[...this.notes.slice(0,updatedIndex),updatedData,...this.notes.slice(updatedIndex+1)];
            console.log(this.notes);
            console.log(updatedData);
            return updatedData;
            
         }
        }
    
    
    
        deleteNote(id){
            let deletedId=this.notes.find((notes)=>notes.id===id);
            console.log("this is the delteed one",deletedId);
            // if(deletedId){
            //     this.notes.splice()
            // }
    
            if(deletedId){
                this.notes=this.notes.filter((note)=>note.id !==id);
                console.log(this.notes);
            }
            
        }
    
        deleteNoteSplice(id){
    
            const index = this.notes.findIndex(note => note.id === id);
    
      if (index !== -1) {
        const deletedNote = this.notes.splice(index, 1)[0];
        console.log(`Note deleted: ${JSON.stringify(deletedNote)}`);
        return true;
      } else {
        console.log(`Note not found for deletion: ${id}`);
        return false;
      }
        }
        
    
    }
    
    module.exports=new Notetaking();
  ```
    const  noteModule=require('./index');


    noteModule.addNote("Hi this is a summy title","This is s summy content");
    noteModule.addNote("Hi this is a second dummy content","This is a second content");
    noteModule.addNote("Hi this is a third dummy content","This is a third content");
    noteModule.updateNote(2,{title:"update title"});
    noteModule.updateNotewithFindINdex(2,{title:"new update"});
    noteModule.deleteNote(2);
    noteModule.deleteNoteSplice(3);

## CRUD two

  ```
          //write your code here
      
      class LibraryManager{
          constructor(){
              this.books=[];
          }
      
          addBook(title,author){
              let book ={
                  title,
                  author
              }
      
              if(!this.books.some((book)=>book.title === title)){
      
                  this.books=[...this.books,book];
                  console.log(`Book added: The ${book.title} by ${book.author}`);
                  return {status:'success'};
                  
              }else {
                  console.log(`Book already exists: The ${book.title}`);
                  return {status:'error'};
                  
              }
          }
      
          listBooks(){
      
              console.log(`Listing all books:\n
              ${this.books}`)
      
              return this.books;
      
          }
      
          removeBook(title){
              if(this.books.some((book)=>book.title === title)){
                this.books=  this.books.filter((book)=>book.title !== title);
                console.log(`Book removed:${title}`);
                return {status:'success'}
              }else{
                  
                  console.log(`Book not found:${title}`);
                  return {status:'error'}
              }
          }
      }
      module.exports=LibraryManager;
```

## Crud with the Promise and the async function:

  ```
          //write your code here
        
        class TrainTicketBooking {
            constructor(){
                this.bookings=[];
            }
        
            addBooking(booking){
                return new Promise((resolve)=>{
                    setTimeout(()=>{
                        this.bookings=[...this.bookings,booking];
                        console.log(`Booking for ${booking.name} added.`);
                        resolve();
        
                    },1000)
                })
            }
        
            getBooking(name){
        
                return new Promise((resolve)=>{
        
                    setTimeout(()=>{
                        const found=this.bookings.find((booking)=>booking.name===name);
                        resolve(found ? found:undefined);
        
        
                    },1000)
        
                })
            }
            listBookings(){
                return new Promise((resolve)=>{
                    setTimeout(
                        ()=>{
        
                            console.log(this.bookings);
                            resolve(this.bookings);
                        }
                    )
                })
            }
        }
        
        
        module.exports=TrainTicketBooking;

    // Another appp
                    const booking=require('./index');
              
              const newBooking=new booking();
              
              // newBooking.addBooking({name:'Alice',destination:'Paris',date:'2024-06-15'});
              // newBooking.addBooking({name:'Berlin',destination:'Berlin',date:'2024-06-16'});
              // newBooking.listBookings();
              
              
              
              // to make them run in the sequential manner we will be using the below given way
              async function testBookings(){
                 await newBooking.addBooking({name:'Alice',destination:'Paris',date:'2024-06-15'});
                 await newBooking.addBooking({name:'Berlin',destination:'Berlin',date:'2024-06-16'});
                 await newBooking.listBookings();
                  
              }
              
              testBookings();
                      
              

```
## CRUD with promise and the sync function with two arrays
```
        //write your code here
        
        class BookMyShow{
        
            constructor(){
        
                this.shows=[];
                this.bookings=[];
            }
            addShow(show){
                return new Promise((resolve)=>{
                    setTimeout(()=>{
                        this.shows=[...this.shows,show];
                        console.log(`Show for ${show.title} added.`);
                        resolve();
            
                    },1000)
                })
            }
        
            listShows(){
                return new Promise((resolve)=>{
                    setTimeout(()=>{
                        console.log(this.shows);
                        resolve(this.shows)
                    },1000)
                })
            }
            bookShow(booking){
                return new Promise((resolve,reject)=>{
                    setTimeout(()=>{
                        const showExists=this.shows.some((show)=>show.title === booking.title);
                        if(showExists){
        
                            this.bookings=[...this.bookings,booking];
                            console.log(`booking for ${booking.title} by ${booking.customer} added.`);
                            resolve();
                        }else{
                            console.log(`Cannot book show: ${booking.title} does not exist.`);
                        return reject(`Show titled "${booking.title}" not found.`);
                        }
        
                    },1000)
                })
            }
        
            listBookings(){
                return new Promise((resolve)=>{
                    setTimeout(()=>{
                        resolve(this.bookings);
                    },1000)
                })
            }
        }
        
        
        module.exports=BookMyShow;

    // app.js
            const book=require('./index');
         const booking =new book();
        
         booking.addShow({title:'Movie A',type:"movie",price:10});
         booking.listShows();
         booking.bookShow({title:'Movie A',customer:'john doe',quantity:2})
         booking.bookShow({title:'Movie B',customer:'john doe',quantity:2})
        
        
         // to handle the aysnc and await of the aychronous data 
        //  async function runApp() {
        //     const app = new BookMyShow();
        
        //     await app.addShow({ title: "Inception", time: "7 PM", screen: 2 });
        
        //     try {
        //         await app.bookShow({ title: "Interstellar", customer: "Ananya" }); // This will fail
        //     } catch (error) {
        //         console.error(`[ERROR]: Booking failed - ${error}`);
        //     }
        
        //     try {
        //         await app.bookShow({ title: "Inception", customer: "Ravi" }); // This will succeed
        //     } catch (error) {
        //         console.error(`[ERROR]: Booking failed - ${error}`);
        //     }
        
        //     const bookings = await app.listBookings();
        //     console.log("Current Bookings:", bookings);
        // }

          
```
## Emitter usage in the code
  ```
      //write your code here
    
    const EventEmitter=require('events')
    
    class Orderprocessor extends EventEmitter{
    
        constructor(){
            super();
            this.orders=[];
        }
    
        placeOrder(orderId){
    
            this.orders.push({id:orderId,status:'placed'});
            this.emit('orderPlaced',orderId);
        }
    
    
        shipOrder(orderId){
            const order=this.orders.find((order)=>order.id===orderId);
            if(order){
                order.status='shipped';
                this.emit('orderShipped',orderId);
            }
        }
    
        deliverOrder(orderId){
            const found=this.orders.find((order)=>order.id===orderId);
            if(found){
                found.status='delivered';
                this.emit('orderDelivered',orderId);
            }
        }
    }
    
    module.exports=Orderprocessor;
```

## Form validation, Mail Validation

  ```
          function formatCheck(email, callback){
          const regex = (/^[^\s@]+@[^\s@]+\.[^\s@]+$/);
          if (regex.test(email)) {
              console.log('Format check passed');
              callback(null, true)
          }
          else{
              console.log('Format check failed');
          callback('Email format is invalid', false);
          }
      }
      function domainCheck(email, callback) {
          const domain = email.split('@')[1];
          if (domain) {
              console.log('Domain check passed');
              callback(null, true)
          }
          else{
              console.log('Domain check failed');
          callback('Email must include a domain', false)
          }
          
      }
      function tldCheck(email , callback){
          const regex = /\.[a-zA-z]{2,}$/;
          if (regex.test(email)) {
              console.log('TLD check passed');
              callback(null, true)
          }
          else{
              console.log('TLD check failed');
          callback('Email must include a valid top-level domain', false)
          }
      }
      function validateEmail(email, callback){
          const checks = [formatCheck, domainCheck, tldCheck];
          let results = [];
          let errorMessages = [];
          function runcheck(index){
              if (index === checks.length) {
                  const isValid = results.every(result => result);
                  console.log('Validation results:', results);
                  callback(errorMessages.length?errorMessages:[], isValid)
                  return;
              }
              checks[index](email,(error, result) => {
                  if (error) {
                      errorMessages.push(error)
                  }
                  results.push(result);
                  runcheck(index+1)
              })
          }
          runcheck(0);
      }
      
      module.exports = {validateEmail}

  ```
  ## JSON functional validators using the Objects concept:
    ```
              const fs=require('fs');
          const jsonString=fs.readFileSync('data.json','utf-8')
          const requiredKeys=['name','age'];
          const keyTypes={name:'string',age:'number'}
          
          function syntaxCheck(jsonString,callback){
              try{
                  if(JSON.parse(jsonString)){
                      console.log("Syntax Check Passed");
                      callback(null,true);
                  }
              }
              catch(error){
                  console.log("Syntax Check Failed");
                  callback("Invalid JSON syntax",false);
              }
          }
          function structureCheck(jsonString,requiredKeys,callback){
              try{
                  const jsonObject=JSON.parse(jsonString);
                  const missingkeys=requiredKeys.filter(key=>!(key in jsonObject));
                  if(missingkeys.length===0){
                      console.log("Structure Check Passed");
                      callback(null,true);
                  }else{
                      console.log(`Structure Check Failed`);
                      callback(`Missing keys: ${missingkeys.join(', ')}`,false);
                  }
              }
          
          catch(error){
              console.log("Syntax Check Failed");
          callback("Invalid JSON Syntax")
          }
          }
          function typeCheck(jsonString,keyTypes,callback){
              try{
                  const jsonObject=JSON.parse(jsonString);
                  const typeErrors=[];
                  Object.entries(keyTypes).forEach(([key,value])=>{
                      const actualType=typeof jsonObject[key];
                      if(value!==actualType){
                          typeErrors.push(`Key '${key}' should be of type ${value}`)
                      }
                  })
                  if(typeErrors.length===0){
                      console.log("Type Check Passed");
                      callback(null,true);
                  }else{
                      console.log(`Type Check Failed`);
                      callback(`${typeErrors}`,false);
                  }
              }
              catch(error){
                  console.log("Syntax Check Failed");
                  callback("Invalid JSON Syntax");
              }
          }
          function validateJSON(jsonString,requiredKeys,keyTypes,callback){
              const checks=[
                  (cb)=>syntaxCheck(jsonString,cb),
                  (cb)=>structureCheck(jsonString,requiredKeys,cb),
                  (cb)=>typeCheck(jsonString,keyTypes,cb),
              ];
              let results=[];
              let errorMessages=[];
              function runCheck(index){
                  if(index===checks.length){
                      const isValid=results.every(res=>res===true);
                      callback(errorMessages,isValid);
                      return;
                  }
                  checks[index]((error,result)=>{
                      if(error)errorMessages.push(error);
                      results.push(result);
                      runCheck(index+1);
                  })
              }
              runCheck(0);
          }
          validateJSON(jsonString,requiredKeys,keyTypes,(errors,isValid)=>{
              if (isValid){
                  console.log("JSON is valid");
              }else{
                  console.log("JSON is invalid");
              }
          })
          module.exports={validateJSON}
  ## Password validator for the same 

  ```
              function lengthCheck(passsword,callback){
        
            if(passsword.length>0){
                console.log("Length Check passed");
                callback(null,true);
            }else{
                console.log("Length Check Failed");
                callback('Password is too short',false);
            }
        
        }
        
        function numberCheck(password,callback){
            const regex=/\d/;
            if(regex.test(password)){
                console.log("Number Check Passed");
                callback(null,true)
            }else{
                console.log("Number Check Failed");
                callback('Password must include at least one number', false)
            }
        }
        
        function specialCharCheck(password,callback){
        
            const regex=/[~!@#$%^&*]/;
            if(regex.test(password)){
                console.log("Special Character Check Passed");
                callback(null,true)
            }else{
                console.log("Special Character Check Failed");
                callback('Password must include at least one special character',false)
            }
        
        }
        
        function upperCaseCheck(password,callback){
            const regex=/[A-Z]/
            if(regex.test(password)){
                console.log("Uppercase Letter Check Passed");
                callback(null,true)
        
            }else{
                console.log("Uppercase Letter Check Failed");
                callback('Password must include at least one uppercase letter',false)
            }
        }
        
        
        function checkPasswordStrength(password,callback){
            const checks=[
                (cb)=>lengthCheck(password,cb),
                (cb)=>numberCheck(password,cb),
                (cb)=>specialCharCheck(password,cb),
                (cb)=>upperCaseCheck(password,cb),
            ]
            const results=[];
            const errorMessages=[];
        
            function runCheck(index){
                if(index == checks.length){
                    const isStrong=results.every(result=>result===true);
                    callback(errorMessages,isStrong);
                    return;
        
                }
                checks[index]((error,result)=>{
                    if(error){errorMessages.push(error);}
                    results.push(result);
                    runCheck(index+1);
                })
        
            }
            runCheck(0);
        }
        
        module.exports=checkPasswordStrength;

  ```
      //app.js
      const checkPasswordStrength = require('./index');
        
        const passwordsToTest = [
            "Abcd123!",       // Strong password
            "abcd123",        // Missing special character and uppercase
            "12345678",       // No letters
            "Pass@word",      // Valid
            "",               // Empty password
        ];
        
        passwordsToTest.forEach(password => {
            console.log(`\nTesting password: "${password}"`);
            checkPasswordStrength(password, (errors, isStrong) => {
                if (isStrong) {
                    console.log("✅ Password is strong");
                } else {
                    console.log("❌ Password is weak. Reasons:");
                    console.log(errors);
                }
            });
        });

  ## How to use forEach to iterate the data 
  ```
          const jobprocessor=require('./jobProcessor');
      
      console.log("Job processing system started.");
      
      const jobs=[{id:1,task:"this is the first task"},
      {id:2,task:"this is the second task"}];
      
      jobs.forEach(job=> jobprocessor.addJob(job));
      
      console.log('Jobs have been added to the queue.');
      jobprocessor.startProcessing(); 
  ```
## To understadn the promise with the async and the settime :

    ```
          // Simulate a movie booking system using Promise + async/await
      
      // 1. Check seat availability (simulate 1-second delay)
      function checkSeat(movie, seat) {
          return new Promise((resolve, reject) => {
              setTimeout(() => {
                  const availableSeats = ['A1', 'A2', 'A3'];
                  if (availableSeats.includes(seat)) {
                      console.log(`✅ Seat ${seat} for ${movie} is available.`);
                      resolve(true);
                  } else {
                      reject(`❌ Seat ${seat} is already booked.`);
                  }
              }, 1000);
          });
      }
      
      // 2. Process payment (simulate 1.5-second delay)
      function processPayment(amount) {
          return new Promise((resolve, reject) => {
              setTimeout(() => {
                  if (amount >= 100) {
                      console.log(`✅ Payment of ₹${amount} successful.`);
                      resolve("TXN12345");
                  } else {
                      reject("❌ Payment failed: Insufficient amount.");
                  }
              }, 1500);
          });
      }
      
      // 3. Confirm booking
      function confirmBooking(movie, seat, txnId) {
          console.log(`🎉 Booking confirmed for ${movie}, Seat ${seat}, TXN ID: ${txnId}`);
      }
      
      // 🔄 Combine all steps using async/await
      async function bookMovieSeat(movie, seat, amount) {
          try {
              await checkSeat(movie, seat);
              const txnId = await processPayment(amount);
              confirmBooking(movie, seat, txnId);
          } catch (error) {
              console.log("🚫 Booking failed:", error);
          }
      }
      
      // Run the simulation
      bookMovieSeat("Avengers: Endgame", "A1", 120); // Valid booking
      // bookMovieSeat("Avengers: Endgame", "B1", 120); // Seat not available
      // bookMovieSeat("Avengers: Endgame", "A2", 50);  // Payment failed


## Upload and download concept 
    ```
            //write your code here
        const fs=require('fs');
        const path=require('path');
        const EventEmitter=require('events');
        
        class FileService extends EventEmitter{
        
            constructor(uploadDir){
                super();
                this.uploadDir=uploadDir;
        
                if(!fs.existsSync(uploadDir)){
                    fs.mkdirSync(uploadDir,{recursive:true})
                }
        
        
            }
        
            uploadFile(fileName,fileContent){
                const filePath=path.join(this.uploadDir,fileName);
                fs.writeFileSync(filePath,fileContent);
                this.emit('fileUploaded', fileName);
                console.log(`File uploaded: ${fileName}`);
        
            }
        
            downloadFile(fileName){
                const filepath=path.join(this.uploadDir,fileName);
                if (!fs.existsSync(filepath)) {
                    throw new Error(`File not found: ${fileName}`);
                }
                this.emit('fileDownloaded', fileName);
                console.log(`File downloaded: ${fileName}`);
                return fs.readFileSync(filepath, 'utf8');
            }
        
        
            streamFileContent(fileName, writableStream) {
                const filePath = path.join(this.uploadDir, fileName);
                if (!fs.existsSync(filePath)) {
                    throw new Error(`File not found: ${fileName}`);
                }
        
                const readable = fs.createReadStream(filePath);
                readable.pipe(writableStream);
        
                this.emit('fileStreamed', fileName);
                console.log(`Streaming file content: ${fileName}`);
            }
        
            
            deleteFile(fileName) {
                const filePath = path.join(this.uploadDir, fileName);
                if (fs.existsSync(filePath)) {
                    fs.unlinkSync(filePath);
                    this.emit('fileDeleted', fileName);
                    console.log(`File deleted: ${fileName}`);
                }
            }
        
            
            listFiles() {
                const files = fs.readdirSync(this.uploadDir);
                this.emit('filesListed', files);
                console.log('Listing files:', files);
                return files;
            }
        
        }
        
        module.exports = FileService;

## how to use the files ,create update and delete 
```
        //write your code here
      
      const fs=require('fs');
      const path=require('path');
      
      const filePath=path.join(__dirname,'test.txt');
      
      const FileOperations={
          writeFile(fileName){
      
              try {
                  
                  fs.writeFileSync(filePath,fileName,'utf-8');
                  console.log("File written successfully.");
              } catch (error) {
                  console.error("Error writing file:", err.message);
                  
              }
      
      
          },
      
          readFile() {
              try {
                  if (!fs.existsSync(filePath)) {
                      return "";
                  }
                  const data = fs.readFileSync(filePath, 'utf8');
                  return data;
              } catch (err) {
                  console.error("Error reading file:", err.message);
                  return "";
              }
          },
      
          deleteFile(){
      
              try {
                  
                  if(fs.existsSync(filePath)){
                      fs.unlinkSync(filePath);
                      console.log("File deleted successfully.");
                  }
              } catch (error) {
                  console.error("Error deleting file:", error.message);
              }
      
          }
      }
      
      // Export the object for external use or testing
      module.exports = FileOperations;
      
      // Sample usage for testing (you can comment this out during test cases)
      if (require.main === module) {
          FileOperations.writeFile("Hello from Node.js!");
          console.log("File Content:", FileOperations.readFile());
          FileOperations.deleteFile();
      }
```
## Currency Conversion
  ```
        const fs=require('fs');
      const os=require('os');
      const path=require('path');
      const util=require('util');
      
      // to promisify the callback function read  
      const readFile= util.promisify(fs.readFile);
      const appendFile=util.promisify(fs.appendFile);
      
      async function getCurrencyRates(){
      
          try {
      const data=await readFile(path.join(__dirname,'data','rates.json'));
      console.log(JSON.parse(data))
      return JSON.parse(data);
      
          } catch (error) {
      
              console.error('Error reading currency rates:', error.message);
              throw new Error('Failed to read currency rates.');
              
          }
      
          
      
      }
      
      async function convertCurrency(amount,fromCurrency,toCurrency){
      
          try {
              const rates=await getCurrencyRates();
              const fromRate=rates[fromCurrency];
              const toRate=rates[toCurrency];
              if(!fromRate || !toRate){
                  throw new Error(`Unsupported currency conversion`);
              }
      
              const converetdAmount=(amount/fromRate)*toRate;
              return converetdAmount;
      
      
              
          } catch (error) {
              console.error('Error converting currency:', error.message);
              throw error;
          }
      }
      
      async function logTransaction(){
      
          const logpath=path.join(__dirname,'data','transactions.log');
          const timestamp = new Date().toISOString();
          const logEntry = `[${timestamp}] ${details}\n`;
      
          try {
              await appendFile(logpath,logEntry,'utf-8')
          } catch (error) {
              console.error('Error logging transaction:', error.message);
              throw new Error('Failed to log transaction.');
              
          }
      
      }
      
      function logSystemInfo(){
          const userInfo = os.userInfo();
          const uptime = os.uptime();
          const platform = os.platform();
          const arch = os.arch();
          const totalMem = os.totalmem();
          const freeMem = os.freemem();
        
          console.log('--- System Information ---');
          console.log(`User: ${userInfo.username}`);
          console.log(`Uptime: ${Math.floor(uptime)} seconds`);
          console.log(`Platform: ${platform}`);
          console.log(`Architecture: ${arch}`);
          console.log(`Total Memory: ${(totalMem / (1024 ** 3)).toFixed(2)} GB`);
          console.log(`Free Memory: ${(freeMem / (1024 ** 3)).toFixed(2)} GB`);
          console.log('--------------------------');
      }
      
      module.exports={
          getCurrencyRates,
          convertCurrency,
          logTransaction,
          logSystemInfo
      }
```
## Money splitter
    ```
      const fs = require('fs');
      const path = require('path');
      const util = require('util');
      
      const readFile = util.promisify(fs.readFile);
      const writeFile = util.promisify(fs.writeFile);
      
      async function getExpenses(){
          try {
              const filePath = path.join(__dirname, 'data', 'expenses.json');
              const data = await readFile(filePath, 'utf-8')
              return JSON.parse(data);
          } catch (error) {
              throw error;
              
          }
      }
      async function calculateSplitExpenses(){
          try {
              const expenses = await getExpenses();
              if(expenses.length == 0) return [];
              const amount = expenses.reduce((sum,expense) => sum+expense.amount, 0)
              const splitAmount = amount/(expenses.length);
              const results = []
              expenses.forEach(expense => {
                  results.push({
                      name: expense.name,
                      amountPaid: expense.amount,
                      amountOwed: splitAmount,
                      balance:parseFloat((expense.amount-splitAmount).toFixed(2))
      
      
                  })
              })
              return results;
          
      
          } catch (error) {
              throw error;
              
          }
      }
      async function saveResults(){
          try {
              const filePath = path.join(__dirname, 'data', 'results.json');
              await writeFile(filePath, JSON.stringify(results,null,2), 'utf-8')
      
          } catch (error) {
              throw error;
              
          }
      
      }
      async function main(){
          try {
              const results = await calculateSplitExpenses();
              console.log("Split Expenses: ",results);
              console.log("Rsults saved successfully.");
      
          } catch (error) {
              throw error;
              
          }
      
      }
      main();
      module.exports = {getExpenses, calculateSplitExpenses, saveResults}
## Middleware function usage and undersatnding
  ```
    const validation = (req, res, next) => {
      const { title, director, releaseYear, genre } = req.body;
    
      // Check if any required field is missing
      if (!title || !director || !releaseYear || !genre) {
        return res.status(400).json({
          success: false,
          message: "Invalid movie data"
        });
      }
    
      // If validation passes, call next middleware
      next();
    };
    
    // Add a movie to the movies list
    const addMovie = (req, res) => {
      // Use the validated movie data from req.body
      const { title, director, releaseYear, genre } = req.body;
      const movie = {
        title,
        director,
        releaseYear,
        genre
      };
    
      // Assuming movies is an array where the movies are stored
      const pushedMovies = movies.push(movie);
    
      // Return the newly added movie
      res.status(201).json({
        success: true,
        data: movie
      });
    };
    
    // Example Express route using the validation middleware and addMovie function
    const express = require('express');
    const app = express();
    app.use(express.json());
    
    let movies = []; // Array to store movies
    
    // Define the route for adding a movie
    app.post('/movies', validation, (req, res) => {
      addMovie(req, res);
    });
    
    const PORT = process.env.PORT || 8080;
    app.listen(PORT, () => {
      console.log(`Server running on port ${PORT}`);
    });
    
