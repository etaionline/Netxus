# Netxus Installation Guide

**Complete setup instructions for the Netxus Intelligence Hub**

## 📋 **Prerequisites**

### **System Requirements**
- Node.js 18+ (Latest LTS recommended)
- npm or yarn package manager
- Chrome browser (for extension installation)
- Git for version control

### **Required Accounts & APIs**
- **Supabase Account**: [supabase.com](https://supabase.com) - Backend services
- **GitHub Account**: [github.com](https://github.com) - Repository management
- **Notion Account**: [notion.so](https://notion.so) - Workspace integration
- **Browser Extension API**: Provided by Netxus team

## 🚀 **Quick Start**

### **1. Clone Repository**
```bash
git clone https://github.com/etaionline/netxus.git
cd netxus
```

### **2. Environment Setup**
```bash
# Copy environment template
cp .env.example .env.local

# Edit environment variables
nano .env.local
```

### **Required Environment Variables**
```env
# Supabase Configuration
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_service_role_key

# GitHub Integration
GITHUB_TOKEN=your_github_personal_access_token

# Notion Integration
NOTION_TOKEN=your_notion_integration_token
NOTION_DATABASE_ID=your_notion_database_id

# Netxus API
NETXUS_API_KEY=your_netxus_api_key
```

## 🏗️ **Detailed Installation**

### **Web Application Setup**

1. **Navigate to web app directory**
   ```bash
   cd web-app
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Database setup**
   ```bash
   # Initialize Supabase
   supabase init
   supabase start
   
   # Run migrations
   supabase db push
   ```

4. **Development server**
   ```bash
   npm run dev
   # Application will be available at http://localhost:3000
   ```

### **Browser Extension Setup**

1. **Navigate to extension directory**
   ```bash
   cd browser-extension
   ```

2. **Install extension dependencies**
   ```bash
   npm install
   ```

3. **Load in Chrome**
   - Open Chrome and navigate to `chrome://extensions/`
   - Enable "Developer mode" toggle
   - Click "Load unpacked"
   - Select the `browser-extension` directory
   - The Netxus extension will appear in your extensions list

4. **Configure extension**
   - Click the Netxus extension icon
   - Enter your Netxus API key
   - Configure target Notion database
   - Test with a web page capture

## 🔧 **Configuration**

### **Supabase Setup**
1. Create new Supabase project
2. Enable Authentication
3. Create required tables (see schema below)
4. Configure Row Level Security policies
5. Set up Edge Functions for AI processing

### **GitHub Integration**
1. Generate Personal Access Token
2. Grant repository access permissions
3. Configure webhooks for automated updates

### **Notion Integration**
1. Create Notion integration
2. Share target databases with integration
3. Copy integration token and database IDs

## 📊 **Database Schema**

### **Core Tables**
```sql
-- AI Agents
CREATE TABLE agents (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  specialty TEXT NOT NULL,
  capabilities TEXT[],
  created_at TIMESTAMP DEFAULT NOW()
);

-- Tasks
CREATE TABLE tasks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  title TEXT NOT NULL,
  description TEXT,
  agent_id UUID REFERENCES agents(id),
  status TEXT DEFAULT 'pending',
  priority TEXT DEFAULT 'medium',
  created_at TIMESTAMP DEFAULT NOW()
);

-- Content Captures
CREATE TABLE captures (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  url TEXT NOT NULL,
  title TEXT,
  content TEXT,
  source_type TEXT,
  processed BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Knowledge Graph
CREATE TABLE entities (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  type TEXT NOT NULL,
  description TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);
```

## 🧪 **Testing Installation**

### **Web Application Tests**
```bash
cd web-app
npm run test
npm run test:e2e
```

### **Extension Tests**
```bash
cd browser-extension
npm run test
```

### **Integration Tests**
1. **Test content capture**: Visit a webpage and click the extension
2. **Verify agent processing**: Check if AI agents process captured content
3. **Test task creation**: Verify tasks appear in dashboard
4. **Check database sync**: Ensure data appears in Notion

## 🚨 **Troubleshooting**

### **Common Issues**

**Issue**: Web app won't start
- **Solution**: Check Node.js version (18+ required)
- **Solution**: Verify environment variables are set correctly

**Issue**: Extension not capturing content
- **Solution**: Verify API key configuration
- **Solution**: Check Notion database permissions

**Issue**: Supabase connection errors
- **Solution**: Verify Supabase URL and keys
- **Solution**: Check database connection in Supabase dashboard

**Issue**: GitHub integration not working
- **Solution**: Verify Personal Access Token permissions
- **Solution**: Check repository access settings

### **Debug Mode**
```bash
# Enable debug logging
DEBUG=netxus:* npm run dev

# Extension debug mode
# Open Chrome DevTools → Extensions → Netxus → Inspect views
```

## 🔐 **Security Considerations**

### **Environment Variables**
- Never commit `.env.local` to version control
- Use different keys for development and production
- Regularly rotate API keys and tokens

### **Supabase Security**
- Enable Row Level Security on all tables
- Use service role key only on server-side
- Configure proper authentication policies

### **Extension Security**
- Extension only captures content you explicitly select
- No automatic data collection without permission
- All API communications are encrypted

## 📈 **Performance Optimization**

### **Web Application**
- Enable Next.js production optimizations
- Configure CDN for static assets
- Optimize database queries with proper indexing

### **Extension**
- Implement content caching
- Optimize API calls with batching
- Use background processing for large captures

## 🚀 **Deployment**

### **Production Deployment**
```bash
# Build for production
cd web-app
npm run build

# Deploy to your preferred platform
# (Vercel, Netlify, AWS, etc.)
```

### **Extension Distribution**
- Package extension for Chrome Web Store
- Submit for review and approval
- Distribute through approved channels

## 📞 **Support**

### **Getting Help**
- **Documentation**: [GitHub Wiki](https://github.com/etaionline/netxus/wiki)
- **Issues**: [GitHub Issues](https://github.com/etaionline/netxus/issues)
- **Discussions**: [GitHub Discussions](https://github.com/etaionline/netxus/discussions)

### **Community**
- Join our Discord server for real-time support
- Follow our blog for updates and tutorials
- Contribute to the project on GitHub

---

## ✅ **Installation Checklist**

- [ ] Node.js 18+ installed
- [ ] Repository cloned successfully
- [ ] Environment variables configured
- [ ] Supabase project set up
- [ ] GitHub integration configured
- [ ] Notion integration configured
- [ ] Web application running locally
- [ ] Browser extension installed and configured
- [ ] Content capture test successful
- [ ] AI agent processing verified
- [ ] Database synchronization working

**Congratulations! Your Netxus Intelligence Hub is now ready to transform your AI workflow.** 🎉