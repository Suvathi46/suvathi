import React, { useState } from "react";
import { motion, AnimatePresence } from "framer-motion";
import {
  Terminal,
  Cpu,
  Database,
  Globe,
  Server,
  Layers,
  Code2,
  ExternalLink,
  Github,
  Mail,
  CheckCircle2,
  Send,
  Play,
  RefreshCw,
} from "lucide-react";

const PROJECTS = [
  {
    id: "proj_01",
    title: "EcoStore MERN E-Commerce",
    endpoint: "GET /api/v1/projects/ecostore",
    tags: ["React", "Node.js", "Express", "MongoDB", "Redux Toolkit"],
    status: "200 OK",
    latency: "45ms",
    description: "Full-featured shopping platform with JWT authentication, Stripe payments, and admin panel.",
    github: "https://github.com",
    live: "https://example.com",
  },
  {
    id: "proj_02",
    title: "TaskPulse Work Management",
    endpoint: "GET /api/v1/projects/taskpulse",
    tags: ["React", "Express", "Socket.io", "MongoDB"],
    status: "200 OK",
    latency: "32ms",
    description: "Real-time collaborative task manager featuring websockets, interactive kanban, and team chat.",
    github: "https://github.com",
    live: "https://example.com",
  },
  {
    id: "proj_03",
    title: "DevMetrics API Analytics Dashboard",
    endpoint: "GET /api/v1/projects/devmetrics",
    tags: ["React", "Tailwind CSS", "Node.js", "Chart.js"],
    status: "200 OK",
    latency: "28ms",
    description: "Developer-focused system health monitoring app featuring live socket streams and dark mode UI.",
    github: "https://github.com",
    live: "https://example.com",
  },
];

const SKILLS = [
  { category: "Frontend", items: ["React.js", "JavaScript (ES6+)", "Tailwind CSS", "Redux", "HTML5/CSS3"], icon: Globe, color: "text-blue-400" },
  { category: "Backend", items: ["Node.js", "Express.js", "RESTful APIs", "JWT Auth", "WebSockets"], icon: Server, color: "text-emerald-400" },
  { category: "Database", items: ["MongoDB", "Mongoose", "Aggregation Framework"], icon: Database, color: "text-amber-400" },
  { category: "Tools & DevOps", items: ["Git / GitHub", "Postman", "Vercel / Render", "NPM"], icon: Cpu, color: "text-purple-400" },
];

export default function Portfolio() {
  const [activeTab, setActiveTab] = useState("dashboard");
  const [selectedProject, setSelectedProject] = useState(PROJECTS[0]);
  const [apiMethod, setApiMethod] = useState("GET");
  const [apiEndpoint, setApiEndpoint] = useState("/api/v1/developer/skills");
  const [apiResponse, setApiResponse] = useState(JSON.stringify(SKILLS, null, 2));
  const [isLoading, setIsLoading] = useState(false);
  const [contactMessage, setContactMessage] = useState("");
  const [contactSent, setContactSent] = useState(false);

  const handleExecuteApi = () => {
    setIsLoading(true);
    setTimeout(() => {
      if (apiEndpoint.includes("projects")) setApiResponse(JSON.stringify(PROJECTS, null, 2));
      else if (apiEndpoint.includes("skills")) setApiResponse(JSON.stringify(SKILLS, null, 2));
      else setApiResponse(JSON.stringify({ status: 200, message: "API Node Active & Ready", timestamp: new Date().toISOString(), developer: "MERN Stack Engineer - Suvathi" }, null, 2));
      setIsLoading(false);
    }, 400);
  };

  const handleSendContact = (e) => {
    e.preventDefault();
    if (!contactMessage.trim()) return;
    setContactSent(true);
    setTimeout(() => { setContactMessage(""); setContactSent(false); }, 3000);
  };

  return (
    <div className="min-h-screen bg-slate-950 text-slate-100 font-mono antialiased flex flex-col">
      <header className="border-b border-slate-800 bg-slate-900/50 backdrop-blur px-6 py-3 flex flex-wrap justify-between items-center gap-4 sticky top-0 z-50">
        <div className="flex items-center space-x-3">
          <div className="flex space-x-1.5"><span className="w-3 h-3 rounded-full bg-red-500/80 inline-block"></span><span className="w-3 h-3 rounded-full bg-amber-500/80 inline-block"></span><span className="w-3 h-3 rounded-full bg-emerald-500/80 inline-block"></span></div>
          <span className="text-xs font-semibold text-slate-400 border-l border-slate-800 pl-3">dev-cluster-01.sys | Suvathi</span>
        </div>
        <div className="flex items-center space-x-6 text-xs text-slate-400">
          <div className="flex items-center space-x-2"><span className="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span><span>SYSTEM: ONLINE</span></div>
          <div className="hidden sm:block"><span>UPTIME: 99.98%</span></div>
          <div className="hidden md:block"><span>STACK: MERN</span></div>
        </div>
      </header>

      <div className="flex-1 flex flex-col md:flex-row">
        <aside className="w-full md:w-64 border-r border-slate-800 bg-slate-900/30 p-4 flex flex-row md:flex-col justify-between gap-2">
          <div className="space-y-1 w-full flex flex-row md:flex-col gap-1 overflow-x-auto">
            <button onClick={() => setActiveTab("dashboard")} className={`flex items-center space-x-3 px-3 py-2.5 rounded-lg text-sm w-full transition ${activeTab === "dashboard"? "bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 font-medium" : "text-slate-400 hover:bg-slate-800/50 hover:text-slate-200"}`}><Layers className="w-4 h-4" /><span>Dashboard</span></button>
            <button onClick={() => setActiveTab("playground")} className={`flex items-center space-x-3 px-3 py-2.5 rounded-lg text-sm w-full transition ${activeTab === "playground"? "bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 font-medium" : "text-slate-400 hover:bg-slate-800/50 hover:text-slate-200"}`}><Terminal className="w-4 h-4" /><span>API Playground</span></button>
            <button onClick={() => setActiveTab("projects")} className={`flex items-center space-x-3 px-3 py-2.5 rounded-lg text-sm w-full transition ${activeTab === "projects"? "bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 font-medium" : "text-slate-400 hover:bg-slate-800/50 hover:text-slate-200"}`}><Code2 className="w-4 h-4" /><span>Projects ({PROJECTS.length})</span></button>
          </div>
          <div className="hidden md:block pt-4 border-t border-slate-800 text-xs text-slate-500"><p>Role: MERN Developer</p><p className="mt-1">Maiyyam Student - Suvathi</p></div>
        </aside>

        <main className="flex-1 p-6 max-w-7xl mx-auto w-full">
          <AnimatePresence mode="wait">
            {activeTab === "dashboard" && (
              <motion.div key="dashboard" initial={{ opacity: 0, y: 10 }} animate={{ opacity: 1, y: 0 }} exit={{ opacity: 0, y: -10 }} className="space-y-8">
                <div className="p-6 rounded-xl border border-slate-800 bg-slate-900/40 relative overflow-hidden">
                  <div className="absolute -top-24 -right-24 w-60 h-60 bg-emerald-500/10 rounded-full blur-3xl"></div>
                  <h1 className="text-3xl font-bold text-white tracking-tight">Hi, I'm Suvathi - MERN Stack Developer</h1>
                  <p className="text-slate-400 mt-2 max-w-2xl font-sans text-sm leading-relaxed">Building robust, scalable full-stack applications with React, Node.js, Express, and MongoDB. Currently specializing in API architecture and dynamic web UIs.</p>
                  <div className="mt-4 flex flex-wrap gap-3">
                    <button onClick={() => setActiveTab("playground")} className="inline-flex items-center space-x-2 text-xs bg-emerald-500 hover:bg-emerald-600 text-slate-950 font-semibold px-4 py-2 rounded-lg transition"><Terminal className="w-3.5 h-3.5" /><span>Test API Playground</span></button>
                    <a href="https://github.com" target="_blank" rel="noreferrer" className="inline-flex items-center space-x-2 text-xs bg-slate-800 hover:bg-slate-700 text-slate-300 px-4 py-2 rounded-lg border border-slate-700 transition"><Github className="w-3.5 h-3.5" /><span>GitHub</span></a>
                  </div>
                </div>

                <div>
                  <h2 className="text-lg font-semibold text-slate-200 mb-4 flex items-center gap-2"><Cpu className="w-5 h-5 text-emerald-400" /><span>System Stack Capabilities</span></h2>
                  <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
                    {SKILLS.map((skill, idx) => {
                      const Icon = skill.icon;
                      return (<div key={idx} className="p-4 rounded-xl border border-slate-800 bg-slate-900/30 hover:border-slate-700 transition"><div className="flex items-center space-x-3 mb-3"><Icon className={`w-5 h-5 ${skill.color}`} /><h3 className="font-semibold text-sm text-slate-200">{skill.category}</h3></div><div className="flex flex-wrap gap-1.5">{skill.items.map((item, i) => (<span key={i} className="text-[11px] bg-slate-800/80 text-slate-300 px-2 py-1 rounded border border-slate-700/50">{item}</span>))}</div></div>);
                    })}
                  </div>
                </div>

                <div>
                  <h2 className="text-lg font-semibold text-slate-200 mb-4 flex items-center gap-2"><Server className="w-5 h-5 text-emerald-400" /><span>Deployed Applications</span></h2>
                  <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
                    {PROJECTS.map((project) => (
                      <div key={project.id} className="p-5 rounded-xl border border-slate-800 bg-slate-900/30 flex flex-col justify-between hover:border-slate-700 transition group">
                        <div><div className="flex items-center justify-between text-xs text-slate-500 mb-2"><span>{project.status}</span><span className="text-emerald-400">{project.latency}</span></div><h3 className="font-bold text-slate-100 group-hover:text-emerald-400 transition">{project.title}</h3><p className="text-xs text-slate-400 font-sans mt-2 line-clamp-3">{project.description}</p></div>
                        <div className="mt-4 pt-4 border-t border-slate-800/80 flex justify-between items-center text-xs"><div className="flex gap-1 flex-wrap">{project.tags.slice(0, 2).map((t, i) => (<span key={i} className="text-[10px] text-slate-400">#{t}</span>))}</div><div className="flex space-x-2"><a href={project.github} target="_blank" rel="noreferrer" className="p-1.5 hover:bg-slate-800 rounded text-slate-400 hover:text-slate-200"><Github className="w-4 h-4" /></a><a href={project.live} target="_blank" rel="noreferrer" className="p-1.5 hover:bg-slate-800 rounded text-slate-400 hover:text-slate-200"><ExternalLink className="w-4 h-4" /></a></div></div>
                      </div>
                    ))}
                  </div>
                </div>

                <div className="p-6 rounded-xl border border-slate-800 bg-slate-900/30">
                  <h2 className="text-lg font-semibold text-slate-200 mb-2 flex items-center gap-2"><Mail className="w-5 h-5 text-emerald-400" /><span>Send Message to Server</span></h2>
                  <p className="text-xs text-slate-400 font-sans mb-4">Dispatch an encrypted transmission or job inquiry straight to my inbox.</p>
                  <form onSubmit={handleSendContact} className="space-y-3">
                    <textarea value={contactMessage} onChange={(e) => setContactMessage(e.target.value)} placeholder="Type your message payload here..." rows={3} className="w-full bg-slate-950 text-slate-200 text-xs p-3 rounded-lg border border-slate-800 focus:border-slate-600 outline-none font-mono"></textarea>
                    <button type="submit" disabled={contactSent} className="bg-emerald-500 hover:bg-emerald-600 text-slate-950 font-bold text-xs px-4 py-2 rounded-lg flex items-center space-x-2 transition">{contactSent? (<><CheckCircle2 className="w-4 h-4" /><span>Payload Delivered!</span></>) : (<><Send className="w-3.5 h-3.5" /><span>POST Message</span></>)}</button>
                  </form>
                </div>
              </motion.div>
            )}

            {activeTab === "playground" && (
              <motion.div key="playground" initial={{ opacity: 0, y: 10 }} animate={{ opacity: 1, y: 0 }} exit={{ opacity: 0, y: -10 }} className="space-y-6">
                <div><h2 className="text-xl font-bold text-white flex items-center gap-2"><Terminal className="w-5 h-5 text-emerald-400" /><span>Interactive API Request Console</span></h2><p className="text-xs text-slate-400 font-sans mt-1">Execute simulated endpoints to fetch profile data in structured JSON format.</p></div>
                <div className="p-4 rounded-xl border border-slate-800 bg-slate-900/50 flex flex-col sm:flex-row gap-2 items-center">
                  <select value={apiMethod} onChange={(e) => setApiMethod(e.target.value)} className="bg-slate-800 text-emerald-400 text-xs font-semibold px-3 py-2 rounded-lg border border-slate-700 outline-none w-full sm:w-auto"><option value="GET">GET</option><option value="POST">POST</option></select>
                  <input type="text" value={apiEndpoint} onChange={(e) => setApiEndpoint(e.target.value)} className="bg-slate-950 text-slate-200 text-xs px-3 py-2 rounded-lg border border-slate-800 flex-1 w-full focus:border-slate-600 outline-none" placeholder="/api/v1/developer/skills" />
                  <button onClick={handleExecuteApi} disabled={isLoading} className="bg-emerald-500 hover:bg-emerald-600 text-slate-950 font-bold text-xs px-5 py-2 rounded-lg flex items-center justify-center space-x-2 transition w-full sm:w-auto">{isLoading? <RefreshCw className="w-4 h-4 animate-spin" /> : <><Play className="w-3.5 h-3.5 fill-current" /><span>Send Request</span></>}</button>
                </div>
                <div className="rounded-xl border border-slate-800 bg-slate-950 overflow-hidden"><div className="bg-slate-900/80 px-4 py-2 border-b border-slate-800 flex justify-between items-center text-xs text-slate-400"><span>Response Output (200 OK)</span><span>application/json</span></div><pre className="p-4 text-xs text-emerald-400 overflow-x-auto max-h-96"><code>{apiResponse}</code></pre></div>
              </motion.div>
            )}

            {activeTab === "projects" && (
              <motion.div key="projects" initial={{ opacity: 0, y: 10 }} animate={{ opacity: 1, y: 0 }} exit={{ opacity: 0, y: -10 }} className="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <div className="space-y-3">
                  <h3 className="text-xs uppercase text-slate-500 font-semibold tracking-wider">Select Endpoint</h3>
                  {PROJECTS.map((p) => (
                    <button key={p.id} onClick={() => setSelectedProject(p)} className={`w-full text-left p-4 rounded-xl border transition ${selectedProject.id === p.id? "bg-emerald-500/10 border-emerald-500/30 text-emerald-300" : "bg-slate-900/30 border-slate-800 text-slate-400 hover:border-slate-700"}`}>
                      <div className="text-xs opacity-70">{p.endpoint}</div>
                      <div className="text-sm font-bold mt-1">{p.title}</div>
                      <div className="flex gap-2 mt-2 text-[10px]"><span>{p.status}</span><span className="text-emerald-400">{p.latency}</span></div>
                    </button>
                  ))}
                </div>

                <div className="lg:col-span-2">
                  <div className="p-6 rounded-xl border border-slate-800 bg-slate-900/40">
                    <div className="flex justify-between items-start">
                      <div><h2 className="text-xl font-bold text-white">{selectedProject.title}</h2><p className="text-xs text-slate-500 mt-1">{selectedProject.endpoint}</p></div>
                      <div className="flex gap-2"><a href={selectedProject.github} target="_blank" rel="noreferrer" className="p-2 bg-slate-800 rounded-lg border border-slate-700 hover:bg-slate-700"><Github className="w-4 h-4" /></a><a href={selectedProject.live} target="_blank" rel="noreferrer" className="p-2 bg-emerald-500 text-slate-950 rounded-lg hover:bg-emerald-600"><ExternalLink className="w-4 h-4" /></a></div>
                    </div>
                    <p className="text-sm text-slate-300 font-sans mt-4 leading-relaxed">{selectedProject.description}</p>
                    <div className="flex flex-wrap gap-2 mt-5">{selectedProject.tags.map((t, i) => (<span key={i} className="text-xs bg-slate-800 text-slate-300 px-3 py-1.5 rounded-full border border-slate-700">{t}</span>))}</div>
                    <div className="mt-6 p-4 rounded-lg bg-slate-950 border border-slate-800"><div className="text-xs text-slate-500 mb-2">System Log</div><div className="text-xs text-emerald-400 font-mono">{`> Building ${selectedProject.id}...`}<br />{`> Status: ${selectedProject.status} | Latency: ${selectedProject.latency}`}<br />{`> Deployment: Successful`}</div></div>
                  </div>
                </div>
              </motion.div>
            )}
          </AnimatePresence>
        </main>
      </div>
    </div>
  );
}
