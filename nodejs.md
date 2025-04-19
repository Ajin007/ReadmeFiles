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
        
