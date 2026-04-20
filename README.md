import React, { useState, useEffect } from 'react';
import { ChevronDown, Github, Linkedin, Mail, ExternalLink, Code, Zap, Database, Tool } from 'lucide-react';

export default function Portfolio() {
  const [scrollY, setScrollY] = useState(0);
  const [activeSection, setActiveSection] = useState('home');
  const [mousePosition, { x, y }] = useState({ x: 0, y: 0 });
  const [selectedProject, setSelectedProject] = useState(null);

  useEffect(() => {
    const handleScroll = () => setScrollY(window.scrollY);
    const handleMouse = (e) => {
      // Use clientX and clientY instead of x and y
      setMousePosition({ clientX: e.clientX, clientY: e.clientY });
    };
    
    window.addEventListener('scroll', handleScroll);
    window.addEventListener('mousemove', handleMouse);
    return () => {
      window.removeEventListener('scroll', handleScroll);
      window.removeEventListener('mousemove', handleMouse);
    };
  }, []);

  const skills = [
    { category: 'Languages', items: ['Python', 'JavaScript', 'TypeScript', 'HTML', 'CSS', 'SQL'] },
    { category: 'Frontend', items: ['React', 'Svelte', 'Tailwind CSS', 'Figma'] },
    { category: 'Backend', items: ['FastAPI', 'Django', 'PostgreSQL', 'MySQL', 'SQLite'] },
    { category: 'Tools', items: ['Git', 'GitLab', 'VSCode', 'Postman'] }
  ];

  const projects = [
    {
      title: 'KCET Rank Map',
      desc: 'Full-stack ML application for ranking prediction',
      tech: ['React', 'Django', 'Python', 'SQLite'],
      image: 'bg-gradient-to-br from-blue-500 to-purple-600',
      accuracy: '~90%',
      link: '#'
    },
    {
      title: 'Version Control System',
      desc: 'Secure proprietary VCS with RBAC',
      tech: ['Svelte', 'FastAPI', 'PostgreSQL'],
      image: 'bg-gradient-to-br from-green-500 to-teal-600',
      features: 'RBAC, Git API Integration',
      link: '#'
    },
    {
      title: 'Analytics Dashboard',
      desc: 'GUI-based analytical tools',
      tech: ['Python', 'Django', 'Matplotlib'],
      image: 'bg-gradient-to-br from-orange-500 to-red-600',
      impact: 'Optimized Matrix Computations',
      link: '#'
    }
  ];

  const experiences = [
    {
      role: 'Software Development Intern',
      company: 'ADE (DRDO)',
      period: 'Feb 2025 – May 2025',
      highlights: ['Svelte & FastAPI Development', 'RBAC Implementation', 'Git API Integration', 'Security Focus'],
      color: 'from-blue-500'
    },
    {
      role: 'Python Development Intern',
      company: 'Tech Company',
      period: 'Oct 2023 – Nov 2023',
      highlights: ['GUI Development', 'Matrix Optimization', 'Data Visualization', 'Automation'],
      color: 'from-purple-500'
    }
  ];

  const StatCard = ({ number, label, icon: Icon }) => (
    <div className="relative group">
      <div className="absolute inset-0 bg-gradient-to-r from-blue-500 to-purple-600 rounded-lg blur opacity-0 group-hover:opacity-75 transition duration-300"></div>
      <div className="relative bg-gray-900 border border-gray-800 rounded-lg p-6 hover:border-purple-500 transition">
        <Icon className="w-8 h-8 text-purple-400 mb-3" />
        <div className="text-3xl font-bold text-white mb-2">{number}</div>
        <div className="text-gray-400 text-sm">{label}</div>
      </div>
    </div>
  );

  const ProjectCard = ({ project, index }) => (
    <div 
      className="group cursor-pointer"
      onClick={() => setSelectedProject(index)}
    >
      <div className="relative bg-gray-900 border border-gray-800 rounded-xl overflow-hidden hover:border-purple-500 transition duration-300 h-64">
        <div className={`absolute inset-0 ${project.image} opacity-10 group-hover:opacity-20 transition`}></div>
        <div className="absolute inset-0 bg-gradient-to-b from-transparent via-transparent to-gray-900"></div>
        
        <div className="relative h-full flex flex-col justify-between p-6">
          <div>
            <h3 className="text-xl font-bold text-white mb-2">{project.title}</h3>
            <p className="text-gray-400 text-sm mb-4">{project.desc}</p>
          </div>
          
          <div className="flex flex-wrap gap-2">
            {project.tech.map((t, i) => (
              <span key={i} className="px-3 py-1 bg-purple-900/50 text-purple-300 text-xs rounded-full border border-purple-700/50">
                {t}
              </span>
            ))}
          </div>
        </div>

        <div className="absolute top-4 right-4 w-10 h-10 bg-purple-600/20 border border-purple-500/50 rounded-lg flex items-center justify-center opacity-0 group-hover:opacity-100 transition">
          <ExternalLink className="w-5 h-5 text-purple-400" />
        </div>
      </div>
    </div>
  );

  return (
    <div className="min-h-screen bg-gray-950 text-white overflow-x-hidden">
      {/* Animated background elements */}
      <div className="fixed inset-0 overflow-hidden pointer-events-none">
        <div className="absolute top-0 left-1/4 w-96 h-96 bg-purple-600/20 rounded-full blur-3xl animate-pulse"></div>
        <div className="absolute bottom-0 right-1/4 w-96 h-96 bg-blue-600/20 rounded-full blur-3xl animate-pulse" style={{ animationDelay: '1s' }}></div>
      </div>

      {/* Navigation */}
      <nav className="fixed top-0 w-full bg-gray-950/80 backdrop-blur-md border-b border-gray-800/50 z-50">
        <div className="max-w-6xl mx-auto px-6 py-4 flex justify-between items-center">
          <div className="text-2xl font-bold bg-gradient-to-r from-purple-400 to-blue-400 bg-clip-text text-transparent">
            BR
          </div>
          <div className="flex gap-8">
            {['Home', 'Skills', 'Projects', 'Experience'].map((item) => (
              <button
                key={item}
                onClick={() => setActiveSection(item.toLowerCase())}
                className={`text-sm font-medium transition ${
                  activeSection === item.toLowerCase()
                    ? 'text-purple-400 border-b-2 border-purple-400'
                    : 'text-gray-400 hover:text-white'
                }`}
              >
                {item}
              </button>
            ))}
          </div>
          <div className="flex gap-4">
            <a href="https://github.com/Bhaskar49ReddyBR" target="_blank" rel="noopener noreferrer" className="p-2 hover:bg-gray-800 rounded-lg transition">
              <Github className="w-5 h-5" />
            </a>
            <a href="https://linkedin.com/in/bhaskar-reddy-b-r-63b83625a/" target="_blank" rel="noopener noreferrer" className="p-2 hover:bg-gray-800 rounded-lg transition">
              <Linkedin className="w-5 h-5" />
            </a>
            <a href="mailto:bhaskarbr710@gmail.com" className="p-2 hover:bg-gray-800 rounded-lg transition">
              <Mail className="w-5 h-5" />
            </a>
          </div>
        </div>
      </nav>

      {/* Hero Section */}
      <section className="relative pt-32 pb-20 px-6">
        <div className="max-w-6xl mx-auto">
          <div className="grid md:grid-cols-2 gap-12 items-center">
            <div className="space-y-6 animate-fadeIn">
              <div className="inline-block">
                <div className="flex items-center gap-3 px-4 py-2 bg-purple-900/30 border border-purple-700/50 rounded-full w-fit">
                  <div className="w-2 h-2 bg-green-400 rounded-full animate-pulse"></div>
                  <span className="text-sm text-purple-300">Available for Opportunities</span>
                </div>
              </div>
              
              <div>
                <h1 className="text-6xl font-bold leading-tight mb-4">
                  Hey, I'm <span className="bg-gradient-to-r from-purple-400 to-blue-400 bg-clip-text text-transparent">Bhaskar</span>
                </h1>
                <p className="text-xl text-gray-400">Full Stack Developer | Python • React • Svelte • FastAPI • ML</p>
              </div>

              <p className="text-lg text-gray-300 leading-relaxed max-w-lg">
                I build scalable, secure, and high-performance web applications. From intuitive frontends to robust backends, I craft solutions that solve real-world problems.
              </p>

              <div className="flex gap-4 pt-4">
                <button className="px-8 py-3 bg-gradient-to-r from-purple-600 to-blue-600 rounded-lg font-medium hover:shadow-lg hover:shadow-purple-500/50 transition transform hover:scale-105">
                  View My Work
                </button>
                <a href="mailto:bhaskarbr710@gmail.com" className="px-8 py-3 border border-purple-500 rounded-lg font-medium hover:bg-purple-900/20 transition">
                  Get in Touch
                </a>
              </div>
            </div>

            {/* Animated code blocks */}
            <div className="relative h-96">
              <div className="absolute inset-0 bg-gradient-to-r from-purple-600/10 to-blue-600/10 rounded-2xl blur-2xl"></div>
              <div className="relative bg-gray-900/50 border border-gray-800/50 rounded-2xl p-6 backdrop-blur space-y-4 animate-slideUp">
                <div className="flex gap-2">
                  <div className="w-3 h-3 rounded-full bg-red-500"></div>
                  <div className="w-3 h-3 rounded-full bg-yellow-500"></div>
                  <div className="w-3 h-3 rounded-full bg-green-500"></div>
                </div>
                <div className="font-mono text-sm space-y-2">
                  <div><span className="text-purple-400">const</span> <span className="text-blue-400">portfolio</span> <span className="text-gray-400">=</span> <span className="text-green-400">{'{ advanced: true }'}</span></div>
                  <div><span className="text-purple-400">const</span> <span className="text-blue-400">skills</span> <span className="text-gray-400">=</span> <span className="text-green-400">['React', 'FastAPI', ...]</span></div>
                  <div><span className="text-purple-400">function</span> <span className="text-blue-400">buildAwesome</span><span className="text-gray-400">() {'{'}</span></div>
                  <div className="pl-4"><span className="text-purple-400">return</span> <span className="text-green-400">'Scalable Web Apps'</span></div>
                  <div><span className="text-gray-400">{'}'}</span></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Stats Section */}
      <section className="py-16 px-6 border-t border-gray-800/50">
        <div className="max-w-6xl mx-auto grid grid-cols-2 md:grid-cols-4 gap-6">
          <StatCard number="5+" label="Years of Coding" icon={Code} />
          <StatCard number="10+" label="Projects Completed" icon={Zap} />
          <StatCard number="8+" label="Technologies" icon={Database} />
          <StatCard number="100%" label="Dedication" icon={Tool} />
        </div>
      </section>

      {/* Skills Section */}
      <section id="skills" className="py-20 px-6 border-t border-gray-800/50">
        <div className="max-w-6xl mx-auto">
          <h2 className="text-4xl font-bold mb-12">Technical Skills</h2>
          <div className="grid md:grid-cols-2 gap-8">
            {skills.map((skillGroup, idx) => (
              <div 
                key={idx}
                className="group bg-gray-900/50 border border-gray-800 rounded-xl p-8 hover:border-purple-500/50 transition hover:bg-gray-800/50"
                style={{ animationDelay: `${idx * 100}ms` }}
              >
                <div className="flex items-center gap-3 mb-6">
                  <div className="w-1 h-8 bg-gradient-to-b from-purple-500 to-blue-500 rounded"></div>
                  <h3 className="text-xl font-bold">{skillGroup.category}</h3>
                </div>
                <div className="flex flex-wrap gap-3">
                  {skillGroup.items.map((skill, i) => (
                    <span
                      key={i}
                      className="px-4 py-2 bg-gray-800/50 border border-gray-700 rounded-lg text-gray-300 hover:bg-purple-900/50 hover:border-purple-500/50 hover:text-purple-300 transition transform hover:scale-110"
                    >
                      {skill}
                    </span>
                  ))}
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Projects Section */}
      <section id="projects" className="py-20 px-6 border-t border-gray-800/50">
        <div className="max-w-6xl mx-auto">
          <h2 className="text-4xl font-bold mb-12">Featured Projects</h2>
          <div className="grid md:grid-cols-3 gap-8">
            {projects.map((project, idx) => (
              <ProjectCard key={idx} project={project} index={idx} />
            ))}
          </div>
        </div>
      </section>

      {/* Experience Section */}
      <section id="experience" className="py-20 px-6 border-t border-gray-800/50">
        <div className="max-w-6xl mx-auto">
          <h2 className="text-4xl font-bold mb-12">Experience</h2>
          <div className="space-y-8">
            {experiences.map((exp, idx) => (
              <div key={idx} className="group">
                <div className="flex items-start gap-6 p-6 bg-gray-900/50 border border-gray-800 rounded-xl hover:border-purple-500/50 transition">
                  <div className={`w-2 h-24 bg-gradient-to-b ${exp.color} to-purple-600 rounded-full opacity-50 group-hover:opacity-100 transition`}></div>
                  <div className="flex-1">
                    <div className="flex justify-between items-start mb-4">
                      <div>
                        <h3 className="text-2xl font-bold mb-1">{exp.role}</h3>
                        <p className="text-purple-400 font-medium">{exp.company}</p>
                      </div>
                      <span className="text-sm text-gray-500">{exp.period}</span>
                    </div>
                    <div className="flex flex-wrap gap-2">
                      {exp.highlights.map((h, i) => (
                        <span key={i} className="px-3 py-1 bg-purple-900/30 text-purple-300 text-sm rounded-full border border-purple-700/50">
                          {h}
                        </span>
                      ))}
                    </div>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* CTA Section */}
      <section className="py-20 px-6 border-t border-gray-800/50">
        <div className="max-w-4xl mx-auto text-center">
          <h2 className="text-5xl font-bold mb-6">Let's Build Something Amazing</h2>
          <p className="text-xl text-gray-400 mb-12">Open to collaborations and exciting new opportunities in full-stack development</p>
          <div className="flex flex-col sm:flex-row gap-4 justify-center">
            <a href="mailto:bhaskarbr710@gmail.com" className="px-10 py-4 bg-gradient-to-r from-purple-600 to-blue-600 rounded-lg font-bold hover:shadow-lg hover:shadow-purple-500/50 transition transform hover:scale-105">
              Start a Project
            </a>
            <a href="https://github.com/Bhaskar49ReddyBR" target="_blank" rel="noopener noreferrer" className="px-10 py-4 border-2 border-purple-500 rounded-lg font-bold hover:bg-purple-900/20 transition">
              View GitHub
            </a>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="border-t border-gray-800/50 py-8 px-6 mt-20">
        <div className="max-w-6xl mx-auto flex justify-between items-center">
          <p className="text-gray-500 text-sm">© 2025 Bhaskar Reddy B R. All rights reserved.</p>
          <div className="flex gap-4">
            <a href="https://github.com/Bhaskar49ReddyBR" className="text-gray-500 hover:text-purple-400 transition">GitHub</a>
            <a href="https://linkedin.com/in/bhaskar-reddy-b-r-63b83625a/" className="text-gray-500 hover:text-purple-400 transition">LinkedIn</a>
            <a href="mailto:bhaskarbr710@gmail.com" className="text-gray-500 hover:text-purple-400 transition">Email</a>
          </div>
        </div>
      </footer>

      {/* Global Styles */}
      <style jsx>{`
        @keyframes fadeIn {
          from {
            opacity: 0;
            transform: translateY(20px);
          }
          to {
            opacity: 1;
            transform: translateY(0);
          }
        }

        @keyframes slideUp {
          from {
            opacity: 0;
            transform: translateY(40px);
          }
          to {
            opacity: 1;
            transform: translateY(0);
          }
        }

        @keyframes float {
          0%, 100% {
            transform: translateY(0px);
          }
          50% {
            transform: translateY(-20px);
          }
        }

        .animate-fadeIn {
          animation: fadeIn 0.6s ease-out;
        }

        .animate-slideUp {
          animation: slideUp 0.8s ease-out;
        }

        .animate-float {
          animation: float 3s ease-in-out infinite;
        }

        ::-webkit-scrollbar {
          width: 10px;
        }

        ::-webkit-scrollbar-track {
          background: rgba(15, 23, 42, 0.5);
        }

        ::-webkit-scrollbar-thumb {
          background: rgba(139, 92, 246, 0.5);
          border-radius: 5px;
        }

        ::-webkit-scrollbar-thumb:hover {
          background: rgba(139, 92, 246, 0.8);
        }
      `}</style>
    </div>
  );
}
