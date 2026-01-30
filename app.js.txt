const $ = (id) => document.getElementById(id);
let all = [];

fetch("photos.json").then(r=>r.json()).then(data=>{
  all=data;
  render();
});

function render(){
  const grid=$("grid");
  grid.innerHTML="";
  all.forEach(it=>{
    const card=document.createElement("div");
    card.className="card";
    card.innerHTML=`
      <img class="thumb" src="${it.thumb}">
      <div class="info">
        <b>${it.title}</b><br>
        <small>${it.date} • ${it.location}</small>
      </div>`;
    card.onclick=()=>openModal(it);
    grid.appendChild(card);
  });
}

function openModal(it){
  $("mImg").src=it.photo;
  $("mTitle").textContent=it.title;
  $("mMeta").textContent=`${it.railroad} • ${it.subdivision} • ${it.location}`;
  $("mTags").innerHTML=it.tags.map(t=>`<span class="tag">${t}</span>`).join("");
  $("mLinks").innerHTML=`<a href="${it.map}" target="_blank">View Map</a>`;
  $("modal").setAttribute("aria-hidden","false");
}

$("close").onclick=()=>{$("modal").setAttribute("aria-hidden","true");};
