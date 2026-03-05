# job-search
<!DOCTYPE html>
<html>
<head>
<title>Job Finder</title>

<style>
body{
font-family:Arial;
background:#f2f2f2;
text-align:center;
}

input{
padding:10px;
margin:10px;
width:220px;
}

button{
padding:10px;
background:green;
color:white;
border:none;
cursor:pointer;
}

.job{
background:white;
padding:15px;
margin:15px auto;
width:350px;
border-radius:10px;
text-align:left;
}
</style>

</head>

<body>

<h1>Job Finder</h1>

<input type="text" id="skill" placeholder="Enter skill (developer, java)">

<br>

<button onclick="findJobs()">Find Jobs</button>

<div id="jobs"></div>

<script>

async function findJobs(){

let skill=document.getElementById("skill").value;

let url="https://www.themuse.com/api/public/jobs"+skill;

try{

let response=await fetch(url);

let data=await response.json();

let jobsHTML="";

data.jobs.slice(0,10).forEach(job=>{

jobsHTML+=`

<div class="job">

<h3>${job.title}</h3>

<p><b>Company:</b> ${job.company_name}</p>

<p><b>Location:</b> ${job.candidate_required_location}</p>

<p><b>Category:</b> ${job.category}</p>

<a href="${job.url}" target="_blank">
<button>Apply</button>
</a>

</div>

`;

});

document.getElementById("jobs").innerHTML=jobsHTML;

}catch(error){

document.getElementById("jobs").innerHTML="Error loading jobs";

}

}

</script>

</body>
</html>
