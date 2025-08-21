---
hide:
  - navigation
  - toc
title: Compute Cloud - Virtual Machines as a Service 
description: Secure and scalable computing capacity for hosting, testing and prototyping your projects
tags:
  - VM
  - Virtual Machine 
  - GPU PaaS
  - Self Service 
  - Cloud Providers
  - AI Training
  - Deep Learning
  - NVIDIA GPUs
  - High Performance Computing
---

<style>
  .hero-banner {
    background: linear-gradient(135deg, var(--md-primary-fg-color) 0%, var(--md-accent-fg-color) 100%);
    color: var(--md-primary-bg-color);
    padding: 2.5rem 1.5rem;
    border-radius: 0.5rem;
    margin: 2rem 0;
    text-align: center;
  }

  .hero-banner h1 {
    font-size: 2.25rem;
    font-weight: 700;
    margin-bottom: 0.75rem;
    color: var(--md-primary-bg-color);
  }

  .hero-banner p {
    font-size: 1.1rem;
    opacity: 0.95;
    margin-bottom: 0;
  }

  #filter-menu {
    text-align: center;
    margin: 1rem 0 2rem 0;
  }

  #filter-menu button {
    margin: 0.3rem;
    padding: 0.4rem 0.9rem;
    border: none;
    border-radius: 0.25rem;
    background: var(--md-accent-fg-color);
    color: white;
    cursor: pointer;
    font-size: 0.85rem;
  }

  #filter-menu button:hover {
    background: var(--md-primary-fg-color);
  }

  .gpu-cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 1rem;
    margin: 2rem 0;
  }

  .gpu-card {
    background: var(--md-code-bg-color);
    border-radius: 0.4rem;
    padding: 0.9rem 1rem;
    border-left: 3px solid var(--md-accent-fg-color);
    transition: transform 0.3s ease;
  }

  .gpu-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 15px rgba(0,0,0,0.08);
  }

  .gpu-card h4 {
    font-size: 1.05rem;
    margin-bottom: 0.2rem;
    color: var(--md-accent-fg-color);
  }

  .gpu-card .subtitle {
    font-size: 0.8rem;
    margin-bottom: 0.6rem;
    color: var(--md-default-fg-color--light);
    font-style: italic;
  }

  @media (max-width: 768px) {
    .hero-banner h1 {
      font-size: 1.75rem;
    }

    .gpu-cards {
      grid-template-columns: 1fr;
    }
  }
</style>

<script>
function filterCards(category) {
  const cards = document.querySelectorAll('.gpu-card');
  cards.forEach(card => {
    const cat = card.getAttribute('data-category');
    card.style.display = (category === 'all' || cat === category) ? 'block' : 'none';
  });
}
</script>

<div class="hero-banner">
  <h1>Virtual Machines as a Service</h1>
  <p>GPU-accelerated virtual machines and block storage for any AI and ML workloads. Provide secure and scalable computing capacity for hosting, testing and prototyping projects.</p>
</div>

<div id="filter-menu">
  <button onclick="filterCards('all')">All</button>
  <button onclick="filterCards('performance')">Performance</button>
  <button onclick="filterCards('networking')">Networking</button>
  <button onclick="filterCards('dev')">Dev Experience</button>
  <button onclick="filterCards('management')">Management</button>
  <button onclick="filterCards('virtualization')">Virtualization</button>
</div>

<div class="gpu-cards">

<div class="gpu-card" data-category="dev">
  <h4>End User Self Service</h4>
  <div class="subtitle">Simple and Intuitive</div>
  End user self-service experience to configure, launch and use a VM with GPUs.
</div>

<div class="gpu-card" data-category="performance">
  <h4>Latest GPU Models</h4>
  <div class="subtitle">From NVIDIA, AMD, and Intel</div>
  Support for state-of-the-art GPU models such as H100, A100, and more.
</div>

<div class="gpu-card" data-category="performance">
  <h4>Scaling</h4>
  <div class="subtitle">Multiple GPUs per VM</div>
  Scale effortlessly from one to eight GPUs in a single virtual machine.
</div>

<div class="gpu-card" data-category="dev">
  <h4>AI/ML Ready OS</h4>
  <div class="subtitle">Quick Deployments</div>
  Accelerate setup with pre-installed AI/ML images, including GPU and network drivers.
</div>

<div class="gpu-card" data-category="management">
  <h4>Block Storage</h4>
  <div class="subtitle">Integrated Storage</div>
  Turnkey integration with Ceph, DDN, Weka, Vast Data, Dell PowerStore, and others.
</div>

<div class="gpu-card" data-category="management">
  <h4>Integrated Metrics</h4>
  <div class="subtitle">Real-Time Usage Monitoring</div>
  View system performance and AI-specific metrics from the user console.
</div>

<div class="gpu-card" data-category="management">
  <h4>Metering</h4>
  <div class="subtitle">Accurate Resource Accounting</div>
  Precise, per-second metering for tracking VM resource usage to support billing and reporting.
</div>

<div class="gpu-card" data-category="networking">
  <h4>VPCs</h4>
  <div class="subtitle">Private Network Support</div>
  Launch VMs inside isolated Virtual Private Clouds with unique CIDR blocks.
</div>

<div class="gpu-card" data-category="networking">
  <h4>Public IPs</h4>
  <div class="subtitle">Direct Internet Connectivity</div>
  Assign public IPs to VMs for external access—no bastion or NAT required.
</div>

<div class="gpu-card" data-category="performance">
  <h4>High Performance</h4>
  <div class="subtitle">Nvidia Reference Architecture Compliant</div>
  Implements and complies with Nvidia's Ref Arch (RA) for high performance GPU passthrough VMs.
</div>

<div class="gpu-card" data-category="virtualization">
  <h4>vGPU Support</h4>
  <div class="subtitle">GPU Virtualization for Shared Access</div>
  Enable GPU sharing across multiple virtual machines using NVIDIA vGPU etc.
</div>

<div class="gpu-card" data-category="performance">
  <h4>SXM GPU Support</h4>
  <div class="subtitle">Maximum Bandwidth & Performance</div>
  Leverage NVIDIA SXM-based GPUs (e.g., H100 SXM, A100 SXM) for extreme performance and bandwidth.
</div>

<div class="gpu-card" data-category="networking">
  <h4>Routing</h4>
  <div class="subtitle">Advanced Traffic Management</div>
  Intelligent traffic routing and load balancing for optimal performance across GPU workloads and regions.
</div>

<div class="gpu-card" data-category="networking">
  <h4>Firewall</h4>
  <div class="subtitle">Network Security Policies</div>
  Comprehensive firewall rules and security policies to protect VM infrastructure and control access.
</div>

<div class="gpu-card" data-category="management">
  <h4>VM Lifecycle Management</h4>
  <div class="subtitle">Automated VM Operations</div>
  Complete lifecycle automation from provisioning to decommissioning with policy-driven management.
</div>

</div>

<!---
Back Button
-->
[← Back](../overview.md){ .md-button .md-button--primary }
