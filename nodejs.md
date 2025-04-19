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

##


