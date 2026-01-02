import React, { useState } from 'react';
import { Plus, Github, ExternalLink, Upload, X, GraduationCap } from 'lucide-react';
import { Button } from '@/components/ui/button';
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card';
import { Dialog, DialogContent, DialogHeader, DialogTitle, DialogTrigger } from '@/components/ui/dialog';
import { Input } from '@/components/ui/input';
import { Textarea } from '@/components/ui/textarea';

interface Project {
  id: string;
  title: string;
  description: string;
  githubUrl: string;
  liveUrl?: string;
  image?: string;
  technologies: string[];
}

const Projects = () => {
  const [projects, setProjects] = useState<Project[]>([
    {
      id: '1',
      title: 'WealthWise',
      description:
        'A personal finance and wealth management web application that helps users track income, expenses, and savings with insightful dashboards.',
      githubUrl: 'https://github.com/ufuos/wealthwise',
      liveUrl: 'https://wealthwise-c28t.onrender.com',
      image:
        'https://images.unsplash.com/photo-1554224155-6726b3ff858f?auto=format&fit=crop&w=800&q=80',
      technologies: ['React', 'Node.js', 'Express', 'MongoDB', 'Chart.js']
    },
    {
      id: '2',
      title: 'E-Commerce Platform',
      description: 'A full-stack e-commerce solution built with React, Node.js, and PostgreSQL.',
      githubUrl: 'https://github.com/username/ecommerce',
      liveUrl: 'https://ecommerce-demo.com',
      image:
        'https://images.unsplash.com/photo-1556742049-0cfed4f6a45d?auto=format&fit=crop&w=800&q=80',
      technologies: ['React', 'Node.js', 'PostgreSQL', 'Stripe']
    },
    {
      id: '3',
      title: 'GlassAdmin (Bubble.io)',
      description:
        'A modern admin panel built with Bubble.io for no-code management of users and projects.',
      githubUrl: '',
      liveUrl:
        'https://bubble.io/page?id=ufuogbe-86355&tab=Design&name=users&ai_generated=true',
      image:
        'https://images.unsplash.com/photo-1605902711622-cfb43c443f5f?auto=format&fit=crop&w=800&q=80',
      technologies: ['No-Code', 'Bubble.io']
    }
  ]);

  const [isDialogOpen, setIsDialogOpen] = useState(false);
  const [newProject, setNewProject] = useState<Partial<Project>>({
    title: '',
    description: '',
    githubUrl: '',
    liveUrl: '',
    technologies: []
  });
  const [newProjectImage, setNewProjectImage] = useState<string>('');

  const handleImageUpload = (event: React.ChangeEvent<HTMLInputElement>) => {
    const file = event.target.files?.[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (e) => setNewProjectImage(e.target?.result as string);
      reader.readAsDataURL(file);
    }
  };

  const handleAddProject = () => {
    if (newProject.title && newProject.description) {
      const project: Project = {
        id: Date.now().toString(),
        title: newProject.title,
        description: newProject.description,
        githubUrl: newProject.githubUrl || '',
        liveUrl: newProject.liveUrl,
        image: newProjectImage,
        technologies: newProject.technologies || []
      };

      setProjects([...projects, project]);
      setNewProject({ title: '', description: '', githubUrl: '', liveUrl: '', technologies: [] });
      setNewProjectImage('');
      setIsDialogOpen(false);
    }
  };

  const handleTechnologiesChange = (value: string) => {
    setNewProject({
      ...newProject,
      technologies: value.split(',').map(t => t.trim()).filter(Boolean)
    });
  };

  return (
    <>
      {/* ================= PROJECTS SECTION ================= */}
      <section id="projects" className="py-20 px-4 bg-gray-50">
        <div className="max-w-7xl mx-auto">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold text-gray-900 mb-4">My Projects</h2>
            <p className="text-xl text-gray-600">
              Selected projects showcasing my full-stack and no-code experience.
            </p>
          </div>

          <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
            {projects.map(project => (
              <Card key={project.id} className="hover:shadow-xl transition">
                {project.image && (
                  <img
                    src={project.image}
                    alt={project.title}
                    className="h-48 w-full object-cover rounded-t-lg"
                  />
                )}

                {project.technologies.includes('No-Code') && (
                  <span className="absolute top-4 left-4 px-2 py-1 bg-yellow-400 text-xs font-semibold rounded-full">
                    No-Code
                  </span>
                )}

                <CardHeader>
                  <CardTitle>{project.title}</CardTitle>
                </CardHeader>

                <CardContent className="space-y-4">
                  <p className="text-gray-600">{project.description}</p>

                  <div className="flex flex-wrap gap-2">
                    {project.technologies.map((tech, i) => (
                      <span
                        key={i}
                        className="px-3 py-1 bg-blue-50 text-blue-700 rounded-full text-xs"
                      >
                        {tech}
                      </span>
                    ))}
                  </div>

                  <div className="flex gap-3 pt-2">
                    {project.githubUrl && (
                      <a href={project.githubUrl} target="_blank">
                        <Github />
                      </a>
                    )}
                    {project.liveUrl && (
                      <a href={project.liveUrl} target="_blank">
                        <ExternalLink />
                      </a>
                    )}
                  </div>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* ================= EDUCATION / CERTIFICATIONS ================= */}
      <section id="education" className="py-20 px-4 bg-white">
        <div className="max-w-5xl mx-auto">
          <div className="text-center mb-12">
            <h2 className="text-4xl font-bold text-gray-900 mb-4">
              Education & Certifications
            </h2>
          </div>

          <div className="space-y-6">
            <Card>
              <CardContent className="flex items-center justify-between py-6">
                <div className="flex items-center gap-4">
                  <GraduationCap className="text-blue-600" />
                  <div>
                    <h3 className="font-semibold">ALX ProDev Backend Engineering</h3>
                    <p className="text-gray-600">Advanced Backend Development Program</p>
                  </div>
                </div>
                <span className="px-3 py-1 bg-green-100 text-green-700 rounded-full text-sm font-medium">
                  Completed 🎓
                </span>
              </CardContent>
            </Card>

            <Card>
              <CardContent className="flex items-center justify-between py-6">
                <div>
                  <h3 className="font-semibold">Full-Stack MERN Development</h3>
                  <p className="text-gray-600">React, Node.js, Express & MongoDB</p>
                </div>
                <span className="px-3 py-1 bg-green-100 text-green-700 rounded-full text-sm font-medium">
                  Completed 🎓
                </span>
              </CardContent>
            </Card>
          </div>
        </div>
      </section>
    </>
  );
};

export default Projects;
