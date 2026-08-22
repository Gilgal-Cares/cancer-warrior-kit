# cancer-warrior-kit
cancer warrior kit app
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cancer Warrior Kit — Gilgal Home Care &amp; Registry</title>
<meta name="description" content="Your private digital companion for diagnosis, treatment, and beyond.">
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2/dist/umd/supabase.js"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@3.19.0/dist/tabler-icons.min.css">
<style>
:root{--navy:#17245B;--purple:#5B3A96;--purp2:#7B5CB8;--wine:#8B2252;--pink:#C4557A;--rose:#E8A0B4;--olive:#5A7A28;--lavender:#EDE8F7;--blush:#FCEEF4;--lilac:#F4EFFC;--mauve:#F8F0F5;--white:#FFFFFF;--cream:#FAF8F5;--surface:#FFFFFF;--surface1:#F7F9FC;--surface2:#FFFFFF;--border:#E2E5F0;--text:#1C1C2E;--text2:#5A6878;--text3:#9CA3B0;}
*{box-sizing:border-box;margin:0;padding:0;}
html,body{height:100%;background:var(--cream);font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;color:var(--text);}
.app{max-width:520px;margin:0 auto;position:relative;min-height:100vh;background:var(--cream);}

.auth-wrap{padding:32px 24px;display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:100vh;}
.auth-logo{width:56px;height:56px;border-radius:16px;background:linear-gradient(135deg,var(--purple),var(--wine));display:flex;align-items:center;justify-content:center;margin-bottom:18px;box-shadow:0 8px 24px rgba(91,58,150,0.3);}
.auth-logo i{font-size:30px;color:white;}
.auth-title{font-size:24px;font-weight:600;text-align:center;margin-bottom:6px;color:var(--navy);}
.auth-sub{font-size:13px;color:var(--text2);text-align:center;margin-bottom:28px;line-height:1.6;max-width:280px;}
.auth-card{background:var(--surface);border-radius:18px;border:1px solid var(--border);padding:26px;width:100%;max-width:360px;box-shadow:0 4px 20px rgba(23,36,91,0.08);}
.auth-err{background:#FEF2F2;color:#DC2626;border-radius:8px;padding:10px 14px;font-size:13px;margin-bottom:14px;border:1px solid #FCA5A5;}
.auth-toggle{text-align:center;margin-top:16px;font-size:13px;color:var(--text2);}
.auth-toggle button{background:none;border:none;cursor:pointer;color:var(--purple);font-weight:600;font-size:13px;}

.top-bar{display:flex;align-items:center;justify-content:space-between;padding:14px 16px 0;gap:12px;background:var(--cream);}
.logo-area{display:flex;align-items:center;gap:10px;}
.logo-dot{width:32px;height:32px;border-radius:10px;background:linear-gradient(135deg,var(--purple),var(--wine));display:flex;align-items:center;justify-content:center;box-shadow:0 4px 12px rgba(91,58,150,0.25);}
.logo-dot i{font-size:17px;color:white;}
.logo-text{font-size:14px;font-weight:600;color:var(--navy);}
.logo-sub{font-size:11px;color:var(--text2);}

.tab-bar{display:flex;gap:6px;padding:14px 16px 0;overflow-x:auto;scrollbar-width:none;background:var(--cream);}
.tab-bar::-webkit-scrollbar{display:none;}
.tab-pill{display:flex;align-items:center;gap:5px;padding:7px 13px;border-radius:100px;border:1px solid var(--border);background:var(--surface);cursor:pointer;white-space:nowrap;font-size:12px;font-weight:500;color:var(--text2);transition:all 0.15s;font-family:inherit;}
.tab-pill.active{background:linear-gradient(135deg,var(--purple),var(--wine));color:white;border-color:transparent;box-shadow:0 4px 12px rgba(91,58,150,0.3);}
.tab-pill i{font-size:14px;}
.content{padding:16px;}

.card{background:var(--surface);border-radius:14px;border:1px solid var(--border);padding:16px 18px;margin-bottom:12px;box-shadow:0 2px 8px rgba(23,36,91,0.05);}
.card-purple{border-left:3px solid var(--purple);}
.card-pink{border-left:3px solid var(--pink);}
.card-wine{border-left:3px solid var(--wine);}
.section-label{font-size:10px;font-weight:600;letter-spacing:0.12em;text-transform:uppercase;color:var(--text2);margin-bottom:8px;margin-top:16px;}
.section-label:first-child{margin-top:0;}

.stat-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:12px;}
.stat-card{border-radius:14px;border:1px solid var(--border);padding:14px;cursor:pointer;transition:all 0.15s;box-shadow:0 2px 8px rgba(23,36,91,0.04);}
.stat-card:hover{transform:translateY(-2px);box-shadow:0 6px 16px rgba(23,36,91,0.1);}
.stat-card:nth-child(1){background:var(--lilac);}
.stat-card:nth-child(2){background:var(--blush);}
.stat-card:nth-child(3){background:var(--lavender);}
.stat-card:nth-child(4){background:linear-gradient(135deg,#EBF3E0,#F7FBF0);}
.stat-num{font-size:24px;font-weight:700;margin-bottom:2px;color:var(--navy);}
.stat-lbl{font-size:12px;color:var(--text2);}
.stat-icon{font-size:20px;margin-bottom:6px;}

.hero{background:linear-gradient(135deg,var(--navy) 0%,var(--purple) 70%,var(--wine) 100%);border-radius:18px;padding:24px 20px;margin-bottom:12px;color:white;box-shadow:0 8px 24px rgba(23,36,91,0.25);}
.hero-label{font-size:10px;letter-spacing:0.14em;text-transform:uppercase;opacity:0.65;margin-bottom:6px;}
.hero-name{font-size:22px;font-weight:600;margin-bottom:4px;}
.hero-sub{font-size:13px;opacity:0.8;}
.hero-dot{display:inline-block;width:7px;height:7px;border-radius:50%;background:var(--rose);margin-right:7px;vertical-align:middle;}

.scripture-card{background:linear-gradient(135deg,var(--lilac),var(--blush));border-radius:14px;border:1px solid #D4C4E8;padding:16px 18px;margin-bottom:12px;}
.scripture-context{font-size:10px;font-weight:600;letter-spacing:0.1em;text-transform:uppercase;color:var(--purple);margin-bottom:8px;}
.scripture-text{font-size:14px;line-height:1.7;color:var(--text);margin-bottom:8px;font-style:italic;}
.scripture-ref{font-size:11px;font-weight:600;color:var(--wine);}

.quick-action{display:flex;align-items:center;gap:12px;padding:14px 16px;background:var(--surface);border-radius:14px;border:1px solid var(--border);cursor:pointer;margin-bottom:8px;transition:all 0.15s;box-shadow:0 2px 8px rgba(23,36,91,0.04);}
.quick-action:hover{border-color:var(--purple);background:var(--lilac);transform:translateX(2px);}
.qa-icon{width:38px;height:38px;border-radius:11px;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.qa-icon i{font-size:18px;}
.qa-label{font-size:14px;font-weight:500;flex:1;}

.btn{display:inline-flex;align-items:center;gap:6px;padding:10px 16px;border-radius:10px;border:1px solid var(--border);background:var(--surface1);cursor:pointer;font-family:inherit;font-size:13px;font-weight:500;color:var(--text);transition:all 0.15s;}
.btn:hover{background:var(--cream);}
.btn:disabled{opacity:0.6;cursor:not-allowed;}
.btn-primary{background:linear-gradient(135deg,var(--purple),var(--wine));color:white;border-color:transparent;width:100%;justify-content:center;box-shadow:0 4px 12px rgba(91,58,150,0.3);}
.btn-primary:hover{opacity:0.92;transform:translateY(-1px);}
.btn-wine{background:var(--wine);color:white;border-color:transparent;}
.btn-olive{background:var(--olive);color:white;border-color:transparent;}
.btn-purple{background:var(--purple);color:white;border-color:transparent;}
.btn-pink{background:linear-gradient(135deg,var(--wine),var(--pink));color:white;border-color:transparent;}
.btn-full{width:100%;justify-content:center;}
.btn-ghost{background:transparent;border:1px solid var(--border);color:var(--text2);}

.badge{display:inline-block;padding:3px 10px;border-radius:100px;font-size:11px;font-weight:600;}
.badge-purple{background:var(--lavender);color:var(--purple);}
.badge-wine{background:var(--blush);color:var(--wine);}
.badge-pink{background:var(--blush);color:var(--pink);}
.badge-olive{background:#EBF3E0;color:var(--olive);}

input,textarea{width:100%;border-radius:10px;border:1px solid var(--border);padding:10px 13px;font-family:inherit;font-size:14px;background:var(--surface1);color:var(--text);outline:none;transition:border-color 0.15s;}
input:focus,textarea:focus{border-color:var(--purple);box-shadow:0 0 0 3px rgba(91,58,150,0.1);}
textarea{resize:vertical;line-height:1.55;}
.field{margin-bottom:13px;}
.field label{display:block;font-size:11px;font-weight:600;letter-spacing:0.08em;text-transform:uppercase;color:var(--text2);margin-bottom:5px;}

.modal-overlay{position:absolute;inset:0;background:rgba(23,36,91,0.5);display:flex;align-items:flex-end;z-index:100;min-height:500px;backdrop-filter:blur(4px);}
.modal-sheet{background:var(--surface);border-radius:22px 22px 0 0;width:100%;padding:22px 20px 36px;max-height:88vh;overflow-y:auto;border-top:3px solid var(--purple);box-shadow:0 -8px 40px rgba(23,36,91,0.15);}
.modal-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:20px;}
.modal-title{font-size:18px;font-weight:600;color:var(--purple);}
.modal-close{background:var(--surface1);border:1px solid var(--border);cursor:pointer;color:var(--text2);font-size:18px;font-family:inherit;line-height:1;padding:6px 8px;border-radius:8px;}

.entry-card{background:var(--surface1);border-radius:12px;border:1px solid var(--border);padding:14px 16px;margin-bottom:10px;}
.del-btn{background:none;border:none;cursor:pointer;color:var(--text3);font-size:16px;font-family:inherit;padding:4px;}
.del-btn:hover{color:var(--wine);}
.divider{height:1px;background:var(--border);margin:18px 0;}
.empty{text-align:center;padding:44px 20px;}
.empty i{font-size:38px;color:var(--rose);display:block;margin-bottom:14px;}
.empty-title{font-size:15px;font-weight:600;margin-bottom:6px;color:var(--navy);}
.empty-sub{font-size:13px;color:var(--text2);}

.book-session{background:linear-gradient(135deg,var(--blush),var(--mauve));border-radius:14px;border:1px solid #D4A0B8;padding:18px;margin-bottom:12px;}
.book-session .lbl{font-size:10px;font-weight:600;letter-spacing:0.1em;text-transform:uppercase;color:var(--wine);margin-bottom:7px;}
.book-session p{font-size:13px;color:var(--text2);line-height:1.55;margin-bottom:14px;}
.book-link{display:block;background:linear-gradient(135deg,var(--wine),var(--pink));color:white;border-radius:10px;padding:12px 0;text-align:center;text-decoration:none;font-size:13px;font-weight:600;box-shadow:0 4px 12px rgba(139,34,82,0.3);}

input[type=range]{accent-color:var(--purple);}
.range-labels{display:flex;justify-content:space-between;font-size:11px;color:var(--text3);margin-top:5px;}
.range-val{font-size:20px;font-weight:600;text-align:center;color:var(--purple);margin-bottom:5px;}

.spin{display:inline-block;animation:spin 0.8s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}
.saving-badge{font-size:11px;color:var(--text2);display:flex;align-items:center;gap:4px;}
.hero-ec{background:linear-gradient(135deg,var(--navy),var(--purple));border-radius:14px;padding:18px;margin-bottom:12px;cursor:pointer;box-shadow:0 6px 20px rgba(23,36,91,0.2);}
</style>
</head>
<body>
<div class="app" id="app"></div>
<script>
const SUPA_URL='https://ztciptzascyfikfbdfnx.supabase.co';
const SUPA_KEY='eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inp0Y2lwdHphc2N5ZmlrZmJkZm54Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODc0MTQ2NjQsImV4cCI6MjEwMjk5MDY2NH0.WataLvZgvpVXDsqWzNXgxLSILxEqYsadUTPJ2mV1wRE';
let sb;
let state={loading:true,user:null,authView:'login',authError:null,authLoading:false,tab:'home',modal:null,form:{},saving:false,data:{profile:null,emergency:null,appointments:[],medications:[],questions:[],symptoms:[],journal:[],gratitude:[],reflections:{},milestones:[]}};

const v=id=>document.getElementById(id)?.value||'';
const uid=()=>state.user?.id;
const name=()=>state.data.profile?.name||state.data.emergency?.name||'Warrior';
function setTab(t){state.tab=t;state.modal=null;state.form={};render();}
function openModal(m,pre){state.modal=m;state.form=pre||{};render();}
function closeModal(){state.modal=null;state.form={};render();}

async function loadAll(){
  if(!uid())return;
  try{
    const[profile,ec,appts,meds,qs,syms,journal,grat,refs,miles]=await Promise.all([
      sb.from('profiles').select('*').eq('id',uid()).single(),
      sb.from('emergency_cards').select('*').eq('user_id',uid()).single(),
      sb.from('appointments').select('*').eq('user_id',uid()).order('created_at',{ascending:false}),
      sb.from('medications').select('*').eq('user_id',uid()).order('created_at',{ascending:false}),
      sb.from('questions').select('*').eq('user_id',uid()).order('created_at',{ascending:false}),
      sb.from('symptoms').select('*').eq('user_id',uid()).order('created_at',{ascending:false}),
      sb.from('journal_entries').select('*').eq('user_id',uid()).order('created_at',{ascending:false}),
      sb.from('gratitude_entries').select('*').eq('user_id',uid()).order('created_at',{ascending:false}),
      sb.from('scripture_reflections').select('*').eq('user_id',uid()),
      sb.from('milestones').select('*').eq('user_id',uid()).order('created_at',{ascending:false}),
    ]);
    const refMap={};(refs.data||[]).forEach(r=>{refMap[r.key]=r.reflection;});
    state.data={profile:profile.data||null,emergency:ec.data||null,appointments:appts.data||[],medications:meds.data||[],questions:qs.data||[],symptoms:syms.data||[],journal:journal.data||[],gratitude:grat.data||[],reflections:refMap,milestones:miles.data||[]};
  }catch(e){console.error(e);}
}

async function signIn(){const email=v('auth_email'),pw=v('auth_pw');if(!email||!pw){state.authError='Please enter email and password.';render();return;}state.authLoading=true;state.authError=null;render();const{error}=await sb.auth.signInWithPassword({email,password:pw});state.authLoading=false;if(error){state.authError=error.message;render();}}
async function signUp(){const email=v('auth_email'),pw=v('auth_pw');if(!email||!pw){state.authError='Please enter email and password.';render();return;}if(pw.length<6){state.authError='Password must be at least 6 characters.';render();return;}state.authLoading=true;state.authError=null;render();const{error}=await sb.auth.signUp({email,password:pw});state.authLoading=false;if(error){state.authError=error.message;render();}}
async function signOut(){await sb.auth.signOut();state.data={profile:null,emergency:null,appointments:[],medications:[],questions:[],symptoms:[],journal:[],gratitude:[],reflections:{},milestones:[]};state.tab='home';state.modal=null;}

async function addItem(table,stateKey,item){state.saving=true;render();const{data,error}=await sb.from(table).insert({...item,user_id:uid()}).select().single();if(!error&&data)state.data[stateKey]=[data,...(state.data[stateKey]||[])];state.saving=false;closeModal();}
async function delItem(table,stateKey,id){await sb.from(table).delete().eq('id',id);state.data[stateKey]=(state.data[stateKey]||[]).filter(x=>x.id!==id);render();}
async function saveEmergencyCard(ec){state.saving=true;render();if(state.data.emergency?.id){await sb.from('emergency_cards').update({...ec,updated_at:new Date()}).eq('id',state.data.emergency.id);state.data.emergency={...state.data.emergency,...ec};}else{const{data}=await sb.from('emergency_cards').insert({...ec,user_id:uid()}).select().single();state.data.emergency=data;}state.saving=false;closeModal();}
async function saveProfile(){const p={name:v('pf_name'),diagnosis:v('pf_diag'),diag_date:v('pf_date')||null};state.saving=true;render();await sb.from('profiles').upsert({...p,id:uid()});state.data.profile={...(state.data.profile||{}),...p};state.saving=false;render();alert('Profile saved ✓');}
async function saveReflection(key,val){state.data.reflections={...state.data.reflections,[key]:val};await sb.from('scripture_reflections').upsert({user_id:uid(),key,reflection:val,updated_at:new Date()},{onConflict:'user_id,key'});}

const TABS=[{id:'home',label:'Home',icon:'ti-home-2'},{id:'medical',label:'Medical',icon:'ti-stethoscope'},{id:'tracker',label:'Track',icon:'ti-chart-line'},{id:'journal',label:'Journal',icon:'ti-writing'},{id:'spiritual',label:'Spiritual',icon:'ti-sparkles'},{id:'milestones',label:'Milestones',icon:'ti-trophy'}];
function mainShell(content){return`<div class="top-bar"><div class="logo-area"><div class="logo-dot"><i class="ti ti-heart-filled"></i></div><div><div class="logo-text">Cancer Warrior Kit</div><div class="logo-sub">${state.data.profile?.name||state.user?.email||''}</div></div></div><div style="display:flex;gap:8px;align-items:center">${state.saving?`<span class="saving-badge"><i class="ti ti-loader spin"></i></span>`:''}<button class="btn" onclick="setTab('settings')" style="padding:7px 10px"><i class="ti ti-settings" style="font-size:16px"></i></button><button class="btn btn-ghost" onclick="signOut()" style="padding:7px 10px" title="Sign out"><i class="ti ti-logout" style="font-size:16px"></i></button></div></div><div class="tab-bar">${TABS.map(t=>`<button class="tab-pill ${state.tab===t.id?'active':''}" onclick="setTab('${t.id}')"><i class="ti ${t.icon}"></i>${t.label}</button>`).join('')}</div><div class="content">${content}</div>`;}

function authHTML(){const isSU=state.authView==='signup';return`<div class="auth-wrap"><div class="auth-logo"><i class="ti ti-heart-filled"></i></div><div class="auth-title">Cancer Warrior Kit</div><div class="auth-sub">Your private companion for diagnosis, treatment, and beyond.</div><div class="auth-card">${state.authError?`<div class="auth-err">${state.authError}</div>`:''}<div class="field"><label>Email</label><input id="auth_email" type="email" placeholder="you@email.com"></div><div class="field"><label>Password</label><input id="auth_pw" type="password" placeholder="${isSU?'Create a password (6+ chars)':'Your password'}"></div><button class="btn btn-primary" onclick="${isSU?'signUp()':'signIn()'}" ${state.authLoading?'disabled':''}>${state.authLoading?'<i class="ti ti-loader spin"></i> Please wait...':isSU?'<i class="ti ti-user-plus"></i> Create account':'<i class="ti ti-login"></i> Sign in'}</button><div class="auth-toggle">${isSU?'Already have an account?':'New here?'} <button onclick="state.authView='${isSU?'login':'signup'}';state.authError=null;render()">${isSU?'Sign in':'Create account'}</button></div></div><div style="margin-top:24px;text-align:center"><div style="font-size:11px;color:var(--text3)">by Gilgal Home Care &amp; Registry · gilgalhomecare.org</div></div></div>`;}

function homeHTML(){const d=state.data;const today=new Date().toLocaleDateString('en-US',{weekday:'long',month:'long',day:'numeric'});return mainShell(`<div class="hero"><div class="hero-label">${today}</div><div class="hero-name"><span class="hero-dot"></span>Welcome, ${name()}</div><div class="hero-sub" style="margin-top:4px">You are not walking this alone. 💜</div></div><div class="scripture-card"><div class="scripture-context"><i class="ti ti-sparkles" style="font-size:11px"></i> Today's Anchor</div><div class="scripture-text">"I can do all things through Christ which strengtheneth me."</div><div class="scripture-ref">— Philippians 4:13 (KJV)</div></div><div class="stat-grid"><div class="stat-card" onclick="setTab('medical')"><div class="stat-icon"><i class="ti ti-calendar" style="color:var(--purple)"></i></div><div class="stat-num">${(d.appointments||[]).length}</div><div class="stat-lbl">Appointments</div></div><div class="stat-card" onclick="setTab('tracker')"><div class="stat-icon"><i class="ti ti-activity" style="color:var(--wine)"></i></div><div class="stat-num">${(d.symptoms||[]).length}</div><div class="stat-lbl">Symptoms logged</div></div><div class="stat-card" onclick="setTab('journal')"><div class="stat-icon"><i class="ti ti-notebook" style="color:var(--purple)"></i></div><div class="stat-num">${(d.journal||[]).length}</div><div class="stat-lbl">Journal entries</div></div><div class="stat-card" onclick="setTab('milestones')"><div class="stat-icon"><i class="ti ti-trophy" style="color:var(--olive)"></i></div><div class="stat-num">${(d.milestones||[]).length}</div><div class="stat-lbl">Milestones</div></div></div><div class="section-label">Quick Actions</div><div class="quick-action" onclick="setTab('tracker')"><div class="qa-icon" style="background:var(--blush)"><i class="ti ti-activity" style="color:var(--wine)"></i></div><div class="qa-label">Log a symptom</div><i class="ti ti-chevron-right" style="color:var(--text3)"></i></div><div class="quick-action" onclick="setTab('journal')"><div class="qa-icon" style="background:var(--lavender)"><i class="ti ti-writing" style="color:var(--purple)"></i></div><div class="qa-label">Add a journal entry</div><i class="ti ti-chevron-right" style="color:var(--text3)"></i></div><div class="quick-action" onclick="setTab('spiritual')"><div class="qa-icon" style="background:var(--blush)"><i class="ti ti-heart" style="color:var(--pink)"></i></div><div class="qa-label">Write a gratitude note</div><i class="ti ti-chevron-right" style="color:var(--text3)"></i></div><div class="quick-action" onclick="setTab('medical')"><div class="qa-icon" style="background:var(--lilac)"><i class="ti ti-calendar-plus" style="color:var(--purp2)"></i></div><div class="qa-label">Record an appointment</div><i class="ti ti-chevron-right" style="color:var(--text3)"></i></div><div class="book-session" style="margin-top:8px"><div class="lbl"><i class="ti ti-calendar-time"></i> Your 30-Minute Session</div><p>Your complimentary 1:1 Cancer Navigation Session with Gabrielle is included with your kit.</p><a class="book-link" href="https://gilgalhomecareandregistry.as.me/?appointmentType=96566627" target="_blank"><i class="ti ti-calendar-event"></i> Book my session</a></div>`);}

function medicalHTML(){const d=state.data;const ec=d.emergency;return mainShell(`<div class="section-label">Emergency Card</div><div class="hero-ec" onclick="openModal('emergency')"><div style="display:flex;justify-content:space-between;align-items:center"><div><div style="font-size:10px;letter-spacing:0.1em;text-transform:uppercase;color:rgba(255,255,255,0.55);margin-bottom:4px">Emergency Card</div><div style="font-size:15px;font-weight:600;color:white">${ec?.name||'Tap to fill in your information'}</div>${ec?.diagnosis?`<div style="font-size:12px;color:rgba(255,255,255,0.65);margin-top:3px">${ec.diagnosis}</div>`:''}</div><i class="ti ti-id" style="font-size:28px;color:rgba(255,255,255,0.35)"></i></div></div><div class="section-label">Appointments</div><button class="btn btn-primary" onclick="openModal('appointment')" style="margin-bottom:10px"><i class="ti ti-plus"></i> Add appointment</button>${!(d.appointments||[]).length?`<div class="empty"><i class="ti ti-calendar"></i><div class="empty-title">No appointments yet</div></div>`:(d.appointments||[]).map(a=>`<div class="entry-card card-purple"><div style="display:flex;justify-content:space-between;align-items:flex-start"><div><span class="badge badge-purple">${a.date||'No date'}</span><div style="font-size:14px;font-weight:500;margin:8px 0 4px">${a.provider||''}</div>${a.reason?`<div style="font-size:13px;color:var(--text2)">${a.reason}</div>`:''}</div><button class="del-btn" onclick="delItem('appointments','appointments','${a.id}')"><i class="ti ti-x"></i></button></div></div>`).join('')}<div class="section-label" style="margin-top:20px">Medications</div><button class="btn btn-purple btn-full" onclick="openModal('medication')" style="margin-bottom:10px"><i class="ti ti-plus"></i> Add medication</button>${!(d.medications||[]).length?`<div class="empty"><i class="ti ti-pill"></i><div class="empty-title">No medications logged</div></div>`:(d.medications||[]).map(m=>`<div class="entry-card card-wine"><div style="display:flex;justify-content:space-between"><div><div style="font-size:14px;font-weight:500">${m.name}</div>${m.dose?`<div style="font-size:12px;color:var(--text2)">${m.dose}${m.frequency?' · '+m.frequency:''}</div>`:''}</div><button class="del-btn" onclick="delItem('medications','medications','${m.id}')"><i class="ti ti-x"></i></button></div></div>`).join('')}<div class="section-label" style="margin-top:20px">Questions for My Doctor</div><button class="btn btn-full" style="margin-bottom:10px;border-color:var(--purple);color:var(--purple)" onclick="openModal('question')"><i class="ti ti-plus"></i> Add a question</button>${(d.questions||[]).map(q=>`<div class="entry-card" style="display:flex;justify-content:space-between;align-items:center;border-left:3px solid var(--pink)"><div style="display:flex;gap:10px;align-items:flex-start"><i class="ti ti-question-mark" style="color:var(--pink);font-size:16px;margin-top:2px;flex-shrink:0"></i><div style="font-size:14px">${q.question}</div></div><button class="del-btn" onclick="delItem('questions','questions','${q.id}')"><i class="ti ti-x"></i></button></div>`).join('')}`);}

function trackerHTML(){const symptoms=state.data.symptoms||[];const sc=n=>{const s=parseInt(n);return s<=3?'var(--olive)':s<=6?'var(--purp2)':'var(--wine)';};const sb2=n=>{const s=parseInt(n);return s<=3?'#EBF3E0':s<=6?'var(--lavender)':'var(--blush)';};return mainShell(`<div style="font-size:13px;color:var(--text2);line-height:1.55;margin-bottom:14px">Rate 1–10. Patterns you notice are often the most useful thing you bring to an appointment.</div><button class="btn btn-pink btn-full" onclick="openModal('symptom')" style="margin-bottom:16px"><i class="ti ti-plus"></i> Log a symptom</button>${!symptoms.length?`<div class="empty"><i class="ti ti-activity"></i><div class="empty-title">No symptoms logged yet</div><div class="empty-sub">Track symptoms to spot patterns over time</div></div>`:symptoms.map(s=>`<div class="entry-card card-pink"><div style="display:flex;justify-content:space-between;align-items:flex-start"><div style="flex:1"><div style="display:flex;gap:8px;align-items:center;margin-bottom:8px"><span style="background:${sb2(s.severity)};color:${sc(s.severity)}" class="badge">${s.severity}/10</span><span style="font-size:11px;color:var(--text3)">${s.date||''}</span></div><div style="font-size:15px;font-weight:500;margin-bottom:4px">${s.symptom}</div>${s.helped?`<div style="font-size:12px;color:var(--text2)">What helped: ${s.helped}</div>`:''}</div><button class="del-btn" onclick="delItem('symptoms','symptoms','${s.id}')"><i class="ti ti-x"></i></button></div></div>`).join('')}`);}

function journalHTML(){const entries=state.data.journal||[];return mainShell(`<div style="font-size:13px;color:var(--text2);line-height:1.55;margin-bottom:14px">A short check-in, once a week. Every entry saves to your private account — your history, yours to keep.</div><button class="btn btn-primary btn-full" onclick="openModal('journal')" style="margin-bottom:16px"><i class="ti ti-writing"></i> New entry</button>${!entries.length?`<div class="empty"><i class="ti ti-notebook"></i><div class="empty-title">No entries yet</div><div class="empty-sub">Your first entry is waiting to be written</div></div>`:entries.map(e=>`<div class="entry-card" style="border-left:3px solid var(--purple);background:var(--lilac)"><div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px"><span class="badge badge-purple">Week of ${e.week||'—'}</span><button class="del-btn" onclick="delItem('journal_entries','journal','${e.id}')"><i class="ti ti-x"></i></button></div>${e.body?`<div style="margin-bottom:10px"><div style="font-size:10px;font-weight:600;text-transform:uppercase;letter-spacing:0.08em;color:var(--purple);margin-bottom:3px">Body</div><div style="font-size:13px;line-height:1.55">${e.body}</div></div>`:''}${e.heart?`<div style="margin-bottom:10px"><div style="font-size:10px;font-weight:600;text-transform:uppercase;letter-spacing:0.08em;color:var(--wine);margin-bottom:3px">Heart &amp; Mind</div><div style="font-size:13px;line-height:1.55">${e.heart}</div></div>`:''}${e.god?`<div style="margin-bottom:10px"><div style="font-size:10px;font-weight:600;text-transform:uppercase;letter-spacing:0.08em;color:var(--purp2);margin-bottom:3px">Where I saw God</div><div style="font-size:13px;line-height:1.55">${e.god}</div></div>`:''}${e.need?`<div style="margin-bottom:10px"><div style="font-size:10px;font-weight:600;text-transform:uppercase;letter-spacing:0.08em;color:var(--pink);margin-bottom:3px">What I need</div><div style="font-size:13px">${e.need}</div></div>`:''}${e.proud?`<div><div style="font-size:10px;font-weight:600;text-transform:uppercase;letter-spacing:0.08em;color:var(--olive);margin-bottom:3px">Proud of</div><div style="font-size:13px">${e.proud}</div></div>`:''}</div>`).join('')}`);}

const SCRIPTURES=[{id:'s1',context:"When you're afraid",verse:"Fear thou not; for I am with thee: be not dismayed; for I am thy God: I will strengthen thee; yea, I will help thee; yea, I will uphold thee with the right hand of my righteousness.",ref:"Isaiah 41:10 (KJV)",color:'var(--navy)'},{id:'s2',context:"When the road feels long",verse:"Yea, though I walk through the valley of the shadow of death, I will fear no evil: for thou art with me; thy rod and thy staff they comfort me.",ref:"Psalm 23:4 (KJV)",color:'var(--purple)'},{id:'s3',context:"When you need hope",verse:"For I know the thoughts that I think toward you, saith the LORD, thoughts of peace, and not of evil, to give you an expected end.",ref:"Jeremiah 29:11 (KJV)",color:'var(--purp2)'},{id:'s4',context:"When you feel too weak",verse:"My grace is sufficient for thee: for my strength is made perfect in weakness.",ref:"2 Corinthians 12:9 (KJV)",color:'var(--wine)'},{id:'s5',context:"When you need to be held",verse:"God is our refuge and strength, a very present help in trouble.",ref:"Psalm 46:1 (KJV)",color:'var(--pink)'}];

function spiritualHTML(){const refs=state.data.reflections||{};const grat=state.data.gratitude||[];return mainShell(`<div class="section-label">Gratitude &amp; Answered Prayers</div><button class="btn btn-pink btn-full" onclick="openModal('gratitude')" style="margin-bottom:12px"><i class="ti ti-heart"></i> Add a gratitude note</button>${grat.slice(0,5).map(g=>`<div class="entry-card card-wine" style="background:var(--blush)"><div style="font-size:10px;font-weight:600;color:var(--wine);margin-bottom:6px">${g.date||''}</div><div style="font-size:13px;line-height:1.55">${g.note}</div></div>`).join('')}${!grat.length?`<div class="empty"><i class="ti ti-heart"></i><div class="empty-title">No gratitude notes yet</div></div>`:''}<div class="divider"></div><div class="section-label">Scripture Reflections</div>${SCRIPTURES.map(s=>`<div class="card" style="border-top:3px solid ${s.color};background:var(--lilac);margin-bottom:14px"><span class="badge badge-purple" style="margin-bottom:10px;display:inline-block">${s.context}</span><div style="font-size:13px;line-height:1.7;color:var(--text);font-style:italic;margin-bottom:8px">"${s.verse}"</div><div style="font-size:11px;font-weight:600;color:${s.color};margin-bottom:12px">— ${s.ref}</div><label style="font-size:10px;font-weight:600;letter-spacing:0.08em;text-transform:uppercase;color:var(--text2);display:block;margin-bottom:6px">Your reflection</label><textarea rows="2" id="ref_${s.id}" oninput="saveReflection('${s.id}',this.value)" placeholder="Write whatever comes...">${refs[s.id]||''}</textarea></div>`).join('')}`);}

function milestonesHTML(){const milestones=state.data.milestones||[];return mainShell(`<div style="font-size:13px;color:var(--text2);line-height:1.55;margin-bottom:14px">Mark how far you've come — you've earned every one of these.</div><button class="btn btn-primary btn-full" onclick="openModal('milestone')" style="margin-bottom:16px"><i class="ti ti-trophy"></i> Add a milestone</button>${milestones.length?`<div class="card" style="background:linear-gradient(135deg,var(--lavender),var(--blush));border-color:#D4C4E8;text-align:center;margin-bottom:16px"><i class="ti ti-award" style="font-size:32px;color:var(--purple);display:block;margin-bottom:8px"></i><div style="font-size:10px;font-weight:600;letter-spacing:0.12em;text-transform:uppercase;color:var(--purple);margin-bottom:6px">You Made It Through</div><div style="font-size:17px;font-weight:600;color:var(--navy);margin-bottom:4px">${name()}</div><div style="font-size:12px;font-style:italic;color:var(--wine);margin-top:8px">"I can do all things through Christ which strengtheneth me." — Phil. 4:13</div></div>`:''} ${!milestones.length?`<div class="empty"><i class="ti ti-star"></i><div class="empty-title">Your milestones await</div><div class="empty-sub">Log your first win — even the small ones count</div></div>`:milestones.map(m=>`<div class="entry-card" style="border-left:3px solid var(--pink);background:var(--blush)"><span class="badge badge-pink">${m.date||'—'}</span><div style="font-size:15px;font-weight:500;margin:8px 0 4px;color:var(--wine)"><i class="ti ti-trophy"></i> ${m.milestone}</div>${m.feeling?`<div style="font-size:12px;color:var(--text2)">How I felt: ${m.feeling}</div>`:''}</div>`).join('')}`);}

function settingsHTML(){const p=state.data.profile||{};return mainShell(`<div style="display:flex;align-items:center;gap:14px;margin-bottom:20px"><div style="width:52px;height:52px;border-radius:50%;background:linear-gradient(135deg,var(--lavender),var(--blush));display:flex;align-items:center;justify-content:center"><i class="ti ti-user" style="font-size:26px;color:var(--purple)"></i></div><div><div style="font-size:16px;font-weight:600">${p.name||'Your Profile'}</div><div style="font-size:12px;color:var(--text2)">${state.user?.email||''}</div></div></div><div class="field"><label>Your Name</label><input id="pf_name" value="${p.name||''}" placeholder="What do you want to be called?"></div><div class="field"><label>Diagnosis</label><input id="pf_diag" value="${p.diagnosis||''}" placeholder="e.g. Stage 4 Breast Cancer"></div><div class="field"><label>Diagnosis Date</label><input type="date" id="pf_date" value="${p.diag_date||''}"></div><button class="btn btn-primary" onclick="saveProfile()" style="margin-bottom:20px"><i class="ti ti-check"></i> Save profile</button><div class="book-session"><div class="lbl"><i class="ti ti-calendar-time"></i> Your Complimentary Session</div><p>Book your 30-minute 1:1 Cancer Navigation Session with Gabrielle.</p><a class="book-link" href="https://gilgalhomecareandregistry.as.me/?appointmentType=96566627" target="_blank"><i class="ti ti-calendar-event"></i> Book my session</a></div><div class="card" style="border-top:3px solid var(--olive)"><div style="font-size:10px;font-weight:600;letter-spacing:0.1em;text-transform:uppercase;color:var(--olive);margin-bottom:6px">Need more support?</div><div style="font-size:13px;color:var(--text2);line-height:1.55;margin-bottom:8px">Gilgal offers ongoing Cancer Navigation, Family Support and Caregiver Coaching, and Medical Appointment Preparation.</div><a href="https://gilgalhomecare.org" target="_blank" style="color:var(--olive);font-size:13px;font-weight:500">gilgalhomecare.org <i class="ti ti-external-link" style="font-size:12px"></i></a></div><button class="btn btn-ghost btn-full" onclick="signOut()" style="margin-top:8px"><i class="ti ti-logout"></i> Sign out</button>`);}

function modalHTML(){if(!state.modal)return'';const wrap=(title,body)=>`<div class="modal-overlay" onclick="closeModal()"><div class="modal-sheet" onclick="event.stopPropagation()"><div class="modal-header"><div class="modal-title">${title}</div><button class="modal-close" onclick="closeModal()"><i class="ti ti-x"></i></button></div>${body}</div></div>`;
if(state.modal==='emergency'){const ec=state.data.emergency||{};return wrap('Emergency Card',`<div class="field"><label>Full Name</label><input id="ec_name" value="${ec.name||''}" placeholder="Your full name"></div><div class="field"><label>Diagnosis</label><input id="ec_diag" value="${ec.diagnosis||''}" placeholder="Stage 4 Breast Cancer"></div><div class="field"><label>Oncologist</label><input id="ec_onco" value="${ec.oncologist||''}" placeholder="Dr. Smith"></div><div class="field"><label>Oncologist Phone</label><input id="ec_oncop" value="${ec.onc_phone||''}" placeholder="(555) 000-0000"></div><div class="field"><label>Current Treatment</label><textarea id="ec_treat" rows="2" placeholder="Chemotherapy, immunotherapy...">${ec.treatment||''}</textarea></div><div class="field"><label>Allergies</label><input id="ec_allergy" value="${ec.allergies||''}" placeholder="Penicillin, latex..."></div><div class="field"><label>Emergency Contact</label><input id="ec_ecn" value="${ec.ec_name||''}" placeholder="Name &amp; relationship"></div><div class="field"><label>Emergency Contact Phone</label><input id="ec_ecp" value="${ec.ec_phone||''}" placeholder="(555) 000-0000"></div><button class="btn btn-primary" onclick="doSaveEC()"><i class="ti ti-device-floppy"></i> Save emergency card</button>`);}
if(state.modal==='appointment')return wrap('New Appointment',`<div class="field"><label>Date</label><input type="date" id="ap_date"></div><div class="field"><label>Provider</label><input id="ap_prov" placeholder="Dr. Smith — Oncology"></div><div class="field"><label>Reason for visit</label><input id="ap_reason" placeholder="Chemo cycle 3, follow-up..."></div><div class="field"><label>Key notes</label><textarea id="ap_notes" rows="2" placeholder="What they said..."></textarea></div><div class="field"><label>Next steps</label><input id="ap_next" placeholder="Labs on Friday..."></div><button class="btn btn-primary" onclick="doAddAppt()"><i class="ti ti-check"></i> Save</button>`);
if(state.modal==='medication')return wrap('Add Medication',`<div class="field"><label>Medication name</label><input id="med_name" placeholder="Taxol, Herceptin..."></div><div class="field"><label>Dose</label><input id="med_dose" placeholder="e.g. 100mg"></div><div class="field"><label>Frequency</label><input id="med_freq" placeholder="Once daily, every 3 weeks..."></div><button class="btn btn-primary" onclick="doAddMed()"><i class="ti ti-check"></i> Save</button>`);
if(state.modal==='question')return wrap('Doctor Question',`<div class="field"><label>Question</label><textarea id="q_text" rows="2" placeholder="What do you want to ask?"></textarea></div><button class="btn btn-primary" onclick="doAddQ()"><i class="ti ti-check"></i> Save</button>`);
if(state.modal==='symptom'){const sev=state.form.severity||5;return wrap('Log a Symptom',`<div class="field"><label>Date</label><input type="date" id="sym_date"></div><div class="field"><label>Symptom</label><input id="sym_name" placeholder="Nausea, fatigue, pain..."></div><div style="margin-bottom:13px"><label style="font-size:11px;font-weight:600;letter-spacing:0.08em;text-transform:uppercase;color:var(--text2);display:block;margin-bottom:8px">Severity</label><div class="range-val" id="sev_val">${sev} / 10</div><input type="range" min="1" max="10" value="${sev}" id="sym_sev" oninput="document.getElementById('sev_val').textContent=this.value+' / 10'"><div class="range-labels"><span>1 — mild</span><span>10 — severe</span></div></div><div class="field"><label>What helped?</label><input id="sym_help" placeholder="Ginger tea, rest, medication..."></div><button class="btn btn-primary" onclick="doAddSym()"><i class="ti ti-check"></i> Save</button>`);}
if(state.modal==='journal')return wrap('Weekly Check-In',`<div class="field"><label>Week of</label><input type="date" id="j_week"></div><div class="field"><label>How is my body feeling?</label><textarea id="j_body" rows="2" placeholder="Physically, how are you doing?"></textarea></div><div class="field"><label>How is my heart and mind?</label><textarea id="j_heart" rows="2" placeholder="Emotionally, what's been present?"></textarea></div><div class="field"><label>Where did I see God show up?</label><textarea id="j_god" rows="2" placeholder="A moment, a person, a feeling..."></textarea></div><div class="field"><label>What do I need more of?</label><input id="j_need" placeholder="Rest, help, quiet, connection..."></div><div class="field"><label>One small thing I'm proud of</label><input id="j_proud" placeholder="You earned this one..."></div><button class="btn btn-primary btn-full" onclick="doAddJournal()"><i class="ti ti-check"></i> Save entry</button>`);
if(state.modal==='gratitude')return wrap('Gratitude &amp; Prayer',`<div class="field"><label>Date</label><input type="date" id="gr_date"></div><div class="field"><label>What I'm grateful for / A prayer answered</label><textarea id="gr_note" rows="4" placeholder="Write it here..."></textarea></div><button class="btn btn-pink btn-full" onclick="doAddGrat()"><i class="ti ti-heart"></i> Save</button>`);
if(state.modal==='milestone')return wrap('Add a Milestone',`<div class="field"><label>Date</label><input type="date" id="ml_date"></div><div class="field"><label>Milestone</label><input id="ml_name" placeholder="Last chemo, clean scan, NEAD, remission..."></div><div class="field"><label>How I felt</label><textarea id="ml_feel" rows="2" placeholder="In your own words..."></textarea></div><button class="btn btn-primary btn-full" onclick="doAddMile()"><i class="ti ti-trophy"></i> Mark this milestone</button>`);
return'';}

function doSaveEC(){saveEmergencyCard({name:v('ec_name'),diagnosis:v('ec_diag'),oncologist:v('ec_onco'),onc_phone:v('ec_oncop'),treatment:v('ec_treat'),allergies:v('ec_allergy'),ec_name:v('ec_ecn'),ec_phone:v('ec_ecp')});}
function doAddAppt(){addItem('appointments','appointments',{date:v('ap_date')||null,provider:v('ap_prov'),reason:v('ap_reason'),notes:v('ap_notes'),followup:v('ap_next')});}
function doAddMed(){addItem('medications','medications',{name:v('med_name'),dose:v('med_dose'),frequency:v('med_freq')});}
function doAddQ(){addItem('questions','questions',{question:v('q_text')});}
function doAddSym(){addItem('symptoms','symptoms',{date:v('sym_date')||null,symptom:v('sym_name'),severity:parseInt(document.getElementById('sym_sev')?.value||'5'),helped:v('sym_help')});}
function doAddJournal(){addItem('journal_entries','journal',{week:v('j_week')||null,body:v('j_body'),heart:v('j_heart'),god:v('j_god'),need:v('j_need'),proud:v('j_proud')});}
function doAddGrat(){addItem('gratitude_entries','gratitude',{date:v('gr_date')||null,note:v('gr_note')});}
function doAddMile(){addItem('milestones','milestones',{date:v('ml_date')||null,milestone:v('ml_name'),feeling:v('ml_feel')});}

function render(){
  const app=document.getElementById('app');
  if(state.loading){app.innerHTML=`<div style="display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:100vh;gap:14px"><div style="width:52px;height:52px;border-radius:16px;background:linear-gradient(135deg,var(--purple),var(--wine));display:flex;align-items:center;justify-content:center;box-shadow:0 8px 24px rgba(91,58,150,0.3)"><i class="ti ti-heart-filled" style="font-size:28px;color:white"></i></div><div style="font-size:14px;color:var(--text2)">Loading your companion…</div></div>`;return;}
  if(!state.user){app.innerHTML=authHTML();return;}
  const screens={home:homeHTML,medical:medicalHTML,tracker:trackerHTML,journal:journalHTML,spiritual:spiritualHTML,milestones:milestonesHTML,settings:settingsHTML};
  app.style.position=state.modal?'relative':'';
  app.innerHTML=(screens[state.tab]||homeHTML)();
  const ex=document.getElementById('modalMount');if(ex)ex.remove();
  if(state.modal){const m=document.createElement('div');m.id='modalMount';m.innerHTML=modalHTML();app.appendChild(m);}
}

window.addEventListener('load',async()=>{
  sb=supabase.createClient(SUPA_URL,SUPA_KEY);
  sb.auth.onAuthStateChange(async(event,session)=>{
    state.user=session?.user||null;
    if(state.user){await loadAll();}
    else{state.data={profile:null,emergency:null,appointments:[],medications:[],questions:[],symptoms:[],journal:[],gratitude:[],reflections:{},milestones:[]};}
    state.loading=false;render();
  });
  const{data:{session}}=await sb.auth.getSession();
  if(!session){state.loading=false;render();}
});
</script>
</body>
</html>
