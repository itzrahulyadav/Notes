*create a new express server

1. create a folder
2. run npm init
3.create a index.js file
4.install express , body-parser and mysql and other dependencies



*use mysql with node

1.npm i mysql
2.require('mysql)

//make a connection

3.const db = mysql.createPool({
    host:'localhost',
    user:'root',
    password:'callmeRe@1B',
    database:'cruddatabase'
});

4.//use post request in mysql

//here movieName and movieReview are coming from the frontend

app.post('/api/insert',(req,res)=> {

    const movieName = req.body.movieName;
    const movieReview = req.body.movieReview;

    const sqlInsert = "INSERT INTO movie_reviews (movieName,movieReview) VALUES (?,?) ";
    db.query(sqlInsert,[movieName,movieReview],(err,result)=>{
        console.log(err);
    })
})

//use update request in mysql

app.put('/api/update',(req,res)=>{
      const name = req.body.movieName;
      const review = req.body.movieReview;

      const sqlUpdate = "UPDATE movie_reviews SET movieReview = ? WHERE movieName = ?";
      db.query(sqlUpdate,[review,name],(err,result)=>{
          if(err)console.log(err);
      })
})

app.delete('/api/delete/:movieName',(req,res)=> {
    const name = req.params.movieName;
    const sqlDelete = "DELETE FROM movie_reviews WHERE movieName = ?";
    db.query(sqlDelete,name,(err,result)=>{
        if(err)console.log(err);
        else console.log("data inserted successfully");
    })
})

//using the functions in react

const submitReview = () => {
       Axios.post('http://localhost:3001/api/insert',{
        movieName:movieName,
        movieReview:movieReview
      })
  }
  const deleteReview = (movie) => {
    Axios.delete(`http://localhost:3001/api/delete/${movie}`);
  }
  const updateReview = (movie) => {
    Axios.put(`http://localhost:3001/api/update`, {
      movieName: movie,
      movieReview: newReview
    });
  }


  useEffect(()=>{
    Axios.get('http://localhost:3001/api/get').then(response =>{
      setMovieList(response.data);
    })
  },[])
