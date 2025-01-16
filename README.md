import React, { useState, useEffect } from 'react';
import { Card, CardHeader, CardContent } from '@/components/ui/card';
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs';
import { Button } from '@/components/ui/button';
import { Alert, AlertTitle, AlertDescription } from '@/components/ui/alert';
import { Progress } from '@/components/ui/progress';
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer } from 'recharts';
import { Settings, HardDrive, Activity, Gauge, AlertTriangle, Database, Shield, Bell } from 'lucide-react';

const GuardianXDashboard = () => {
  // State management for different data types
  const [activeTab, setActiveTab] = useState('overview');
  const [systemMetrics, setSystemMetrics] = useState({
    cpu: 45,
    memory: 60,
    disk: 75,
    network: 30,
    temperature: 42
  });
  const [securityEvents, setSecurityEvents] = useState([]);
  const [notifications, setNotifications] = useState([]);
  const [systemInfo, setSystemInfo] = useState({
    systemName: 'Primary System',
    osType: 'Windows 11 Pro',
    osVersion: '21H2',
    cpuModel: 'Intel Core i7-12700K',
    totalRam: 32,
    totalStorage: 1000
  });

  // Simulated historical data
  const performanceHistory = [
    { time: '00:00', cpu: 40, memory: 55, disk: 70, network: 25 },
    { time: '00:05', cpu: 45, memory: 60, disk: 75, network: 30 },
    { time: '00:10', cpu: 42, memory: 58, disk: 72, network: 28 },
    { time: '00:15', cpu: 48, memory: 62, disk: 78, network: 35 }
  ];

  // Simulated security events
  const recentSecurityEvents = [
    { id: 1, type: 'Malware Scan', status: 'Completed', findings: 'No threats found', timestamp: '2025-01-16 10:30:00' },
    { id: 2, type: 'Firewall', status: 'Alert', findings: 'Blocked suspicious connection', timestamp: '2025-01-16 10:15:00' }
  ];

  return (
    <div className="w-full max-w-7xl mx-auto p-4">
      {/* Header with branding */}
      <header className="mb-8">
        <div className="space-y-2">
          <div className="flex items-center space-x-2">
            <h1 className="text-5xl font-black bg-gradient-to-r from-indigo-600 via-purple-500 to-blue-500 bg-clip-text text-transparent tracking-tight">GUARDIAN-X</h1>
            <span className="bg-gradient-to-r from-indigo-600 to-purple-600 text-white px-3 py-1 rounded-full text-sm font-semibold">Elite</span>
          </div>
          <p className="text-lg text-gray-600 font-medium">Global Unified Active Real-time Defense & Intelligent Analysis Network</p>
          <div className="flex items-center space-x-4">
            <span className="text-sm text-purple-600 font-semibold">eXtended Protection</span>
            <span className="text-sm text-gray-400">|</span>
            <span className="text-sm text-gray-600">Enterprise Edition 2025</span>
          </div>
        </div>
      </header>

      {/* Main dashboard content */}
      <Tabs value={activeTab} onValueChange={setActiveTab} className="space-y-4">
        <TabsList className="grid grid-cols-6 gap-4">
          <TabsTrigger value="overview" className="flex items-center">
            <Gauge className="w-4 h-4 mr-2" />
            Overview
          </TabsTrigger>
          <TabsTrigger value="performance" className="flex items-center">
            <Activity className="w-4 h-4 mr-2" />
            Performance
          </TabsTrigger>
          <TabsTrigger value="security" className="flex items-center">
            <Shield className="w-4 h-4 mr-2" />
            Security
          </TabsTrigger>
          <TabsTrigger value="storage" className="flex items-center">
            <HardDrive className="w-4 h-4 mr-2" />
            Storage
          </TabsTrigger>
          <TabsTrigger value="database" className="flex items-center">
            <Database className="w-4 h-4 mr-2" />
            Database
          </TabsTrigger>
          <TabsTrigger value="notifications" className="flex items-center">
            <Bell className="w-4 h-4 mr-2" />
            Alerts
          </TabsTrigger>
        </TabsList>

        {/* Overview Tab Content */}
        <TabsContent value="overview">
          <div className="grid grid-cols-2 gap-4">
            <Card>
              <CardHeader>
                <h3 className="text-lg font-semibold">System Health Overview</h3>
              </CardHeader>
              <CardContent>
                <div className="space-y-4">
                  <div>
                    <div className="flex items-center justify-between mb-2">
                      <span className="flex items-center">
                        <Activity className="w-4 h-4 mr-2" />
                        CPU Usage
                      </span>
                      <span>{systemMetrics.cpu}%</span>
                    </div>
                    <Progress value={systemMetrics.cpu} className="bg-gray-100" />
                  </div>
                  <div>
                    <div className="flex items-center justify-between mb-2">
                      <span className="flex items-center">
                        <Gauge className="w-4 h-4 mr-2" />
                        Memory Usage
                      </span>
                      <span>{systemMetrics.memory}%</span>
                    </div>
                    <Progress value={systemMetrics.memory} className="bg-gray-100" />
                  </div>
                  <div>
                    <div className="flex items-center justify-between mb-2">
                      <span className="flex items-center">
                        <HardDrive className="w-4 h-4 mr-2" />
                        Disk Usage
                      </span>
                      <span>{systemMetrics.disk}%</span>
                    </div>
                    <Progress value={systemMetrics.disk} className="bg-gray-100" />
                  </div>
                </div>
              </CardContent>
            </Card>

            <Card>
              <CardHeader>
                <h3 className="text-lg font-semibold">Performance History</h3>
              </CardHeader>
              <CardContent>
                <ResponsiveContainer width="100%" height={250}>
                  <LineChart data={performanceHistory}>
                    <CartesianGrid strokeDasharray="3 3" />
                    <XAxis dataKey="time" />
                    <YAxis />
                    <Tooltip />
                    <Legend />
                    <Line type="monotone" dataKey="cpu" stroke="#8884d8" name="CPU" />
                    <Line type="monotone" dataKey="memory" stroke="#82ca9d" name="Memory" />
                    <Line type="monotone" dataKey="disk" stroke="#ffc658" name="Disk" />
                  </LineChart>
                </ResponsiveContainer>
              </CardContent>
            </Card>
          </div>

          {/* System Information */}
          <Card className="mt-4">
            <CardHeader>
              <h3 className="text-lg font-semibold">System Information</h3>
            </CardHeader>
            <CardContent>
              <div className="grid grid-cols-3 gap-4">
                <div>
                  <p className="text-sm text-gray-500">System Name</p>
                  <p className="font-medium">{systemInfo.systemName}</p>
                </div>
                <div>
                  <p className="text-sm text-gray-500">Operating System</p>
                  <p className="font-medium">{systemInfo.osType}</p>
                </div>
                <div>
                  <p className="text-sm text-gray-500">CPU Model</p>
                  <p className="font-medium">{systemInfo.cpuModel}</p>
                </div>
                <div>
                  <p className="text-sm text-gray-500">Total RAM</p>
                  <p className="font-medium">{systemInfo.totalRam} GB</p>
                </div>
                <div>
                  <p className="text-sm text-gray-500">Total Storage</p>
                  <p className="font-medium">{systemInfo.totalStorage} GB</p>
                </div>
              </div>
            </CardContent>
          </Card>

          {/* Recent Security Events */}
          <Card className="mt-4">
            <CardHeader>
              <h3 className="text-lg font-semibold">Recent Security Events</h3>
            </CardHeader>
            <CardContent>
              <div className="space-y-4">
                {recentSecurityEvents.map(event => (
                  <div key={event.id} className="flex items-center justify-between p-4 bg-gray-50 rounded-lg">
                    <div>
                      <p className="font-medium">{event.type}</p>
                      <p className="text-sm text-gray-500">{event.findings}</p>
                    </div>
                    <div className="text-right">
                      <p className={`text-sm ${event.status === 'Alert' ? 'text-red-500' : 'text-green-500'}`}>
                        {event.status}
                      </p>
                      <p className="text-xs text-gray-500">{event.timestamp}</p>
                    </div>
                  </div>
                ))}
              </div>
            </CardContent>
          </Card>
        </TabsContent>

        {/* System Repair Tab */}
        <TabsContent value="repair">
          <div className="grid grid-cols-2 gap-4">
            <Card>
              <CardHeader>
                <h3 className="text-lg font-semibold">Quick System Diagnostics</h3>
              </CardHeader>
              <CardContent>
                <div className="space-y-4">
                  <div className="p-4 bg-blue-50 rounded-lg">
                    <h4 className="font-medium text-blue-700">Windows Version Detected</h4>
                    <p className="text-sm text-blue-600">Windows 11 Pro (Build 22621.1702)</p>
                  </div>
                  
                  <div className="grid grid-cols-2 gap-3">
                    {[
                      { name: 'System Files', status: 'Healthy', icon: 'Files' },
                      { name: 'Disk Space', status: 'Warning', icon: 'Storage' },
                      { name: 'Network', status: 'Healthy', icon: 'Network' },
                      { name: 'Startup', status: 'Attention', icon: 'Boot' }
                    ].map((check) => (
                      <div key={check.name} className="p-3 bg-gray-50 rounded-lg">
                        <p className="font-medium">{check.name}</p>
                        <p className={`text-sm ${
                          check.status === 'Healthy' ? 'text-green-600' :
                          check.status === 'Warning' ? 'text-yellow-600' :
                          'text-red-600'
                        }`}>{check.status}</p>
                      </div>
                    ))}
                  </div>
                </div>
              </CardContent>
            </Card>

            <Card>
              <CardHeader>
                <h3 className="text-lg font-semibold">Automated Repair Tools</h3>
              </CardHeader>
              <CardContent>
                <div className="space-y-3">
                  {[
                    { name: 'System File Check', cmd: 'sfc /scannow', time: '15-20 minutes' },
                    { name: 'Disk Cleanup', cmd: 'cleanmgr', time: '5-10 minutes' },
                    { name: 'DISM Health Check', cmd: 'DISM /Online /Cleanup-Image /CheckHealth', time: '10-15 minutes' },
                    { name: 'Network Reset', cmd: 'netsh winsock reset', time: '2-5 minutes' }
                  ].map((tool) => (
                    <div key={tool.name} className="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                      <div>
                        <p className="font-medium">{tool.name}</p>
                        <p className="text-sm text-gray-500">Est. time: {tool.time}</p>
                      </div>
                      <Button variant="outline" size="sm">Run</Button>
                    </div>
                  ))}
                </div>
              </CardContent>
            </Card>
          </div>

          <Card className="mt-4">
            <CardHeader>
              <h3 className="text-lg font-semibold">System Maintenance Tasks</h3>
            </CardHeader>
            <CardContent>
              <div className="space-y-4">
                <div className="grid grid-cols-3 gap-4">
                  {/* Disk Cleanup */}
                  <Card>
                    <CardHeader>
                      <h4 className="text-md font-medium">Disk Cleanup</h4>
                    </CardHeader>
                    <CardContent>
                      <div className="space-y-2">
                        <p className="text-sm text-gray-500">Clean temporary files, downloads, and recycle bin</p>
                        <Button className="w-full" variant="outline">Start Cleanup</Button>
                      </div>
                    </CardContent>
                  </Card>

                  {/* Startup Management */}
                  <Card>
                    <CardHeader>
                      <h4 className="text-md font-medium">Startup Programs</h4>
                    </CardHeader>
                    <CardContent>
                      <div className="space-y-2">
                        <p className="text-sm text-gray-500">Manage and optimize startup applications</p>
                        <Button className="w-full" variant="outline">Manage Startup</Button>
                      </div>
                    </CardContent>
                  </Card>

                  {/* Network Reset */}
                  <Card>
                    <CardHeader>
                      <h4 className="text-md font-medium">Network Reset</h4>
                    </CardHeader>
                    <CardContent>
                      <div className="space-y-2">
                        <p className="text-sm text-gray-500">Reset network adapters and configurations</p>
                        <Button className="w-full" variant="outline">Reset Network</Button>
                      </div>
                    </CardContent>
                  </Card>
                </div>

                {/* Scheduled Maintenance */}
                <Card>
                  <CardHeader>
                    <h4 className="text-md font-medium">Scheduled Maintenance</h4>
                  </CardHeader>
                  <CardContent>
                    <div className="space-y-3">
                      {[
                        { task: 'Weekly Disk Cleanup', schedule: 'Every Sunday at 2 AM', status: 'Active' },
                        { task: 'Monthly System Check', schedule: 'First day of month at 3 AM', status: 'Active' },
                        { task: 'Daily Quick Scan', schedule: 'Daily at 12 PM', status: 'Active' }
                      ].map((maintenance, i) => (
                        <div key={i} className="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                          <div>
                            <p className="font-medium">{maintenance.task}</p>
                            <p className="text-sm text-gray-500">{maintenance.schedule}</p>
                          </div>
                          <span className="px-2 py-1 bg-green-100 text-green-700 rounded-full text-sm">
                            {maintenance.status}
                          </span>
                        </div>
                      ))}
                    </div>
                  </CardContent>
                </Card>
              </div>
            </CardContent>
          </Card>
        </TabsContent>

        {/* Performance Tab Content */}
        <TabsContent value="performance">
          <div className="grid grid-cols-2 gap-4">
            <Card>
              <CardHeader>
                <h3 className="text-lg font-semibold">CPU Performance</h3>
              </CardHeader>
              <CardContent>
                <ResponsiveContainer width="100%" height={200}>
                  <LineChart data={performanceHistory}>
                    <CartesianGrid strokeDasharray="3 3" />
                    <XAxis dataKey="time" />
                    <YAxis />
                    <Tooltip />
                    <Line type="monotone" dataKey="cpu" stroke="#8884d8" name="CPU Usage" />
                  </LineChart>
                </ResponsiveContainer>
                <div className="mt-4 grid grid-cols-2 gap-4">
                  <div className="p-3 bg-gray-50 rounded-lg">
                    <p className="text-sm text-gray-500">Current Speed</p>
                    <p className="text-xl font-bold">3.8 GHz</p>
                  </div>
                  <div className="p-3 bg-gray-50 rounded-lg">
                    <p className="text-sm text-gray-500">Temperature</p>
                    <p className="text-xl font-bold">65°C</p>
                  </div>
                </div>
              </CardContent>
            </Card>

            <Card>
              <CardHeader>
                <h3 className="text-lg font-semibold">Memory Analysis</h3>
              </CardHeader>
              <CardContent>
                <div className="mb-4">
                  <div className="flex justify-between mb-2">
                    <span>Memory Usage</span>
                    <span>12.8 GB / 32 GB</span>
                  </div>
                  <Progress value={40} className="h-2" />
                </div>
                <div className="grid grid-cols-2 gap-4">
                  <div className="p-3 bg-gray-50 rounded-lg">
                    <p className="text-sm text-gray-500">Available</p>
                    <p className="text-xl font-bold">19.2 GB</p>
                  </div>
                  <div className="p-3 bg-gray-50 rounded-lg">
                    <p className="text-sm text-gray-500">Cached</p>
                    <p className="text-xl font-bold">4.8 GB</p>
                  </div>
                </div>
              </CardContent>
            </Card>
          </div>

          <Card className="mt-4">
            <CardHeader>
              <h3 className="text-lg font-semibold">Process Monitor</h3>
            </CardHeader>
            <CardContent>
              <div className="space-y-3">
                {[
                  { name: 'System', cpu: 2.5, memory: 850, pid: 4 },
                  { name: 'Chrome', cpu: 15.2, memory: 1240, pid: 1356 },
                  { name: 'VS Code', cpu: 8.7, memory: 980, pid: 2145 },
                ].map(process => (
                  <div key={process.pid} className="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                    <div>
                      <p className="font-medium">{process.name}</p>
                      <p className="text-sm text-gray-500">PID: {process.pid}</p>
                    </div>
                    <div className="text-right">
                      <p>CPU: {process.cpu}%</p>
                      <p>Memory: {process.memory} MB</p>
                    </div>
                  </div>
                ))}
              </div>
            </CardContent>
          </Card>
        </TabsContent>

        {/* Security Tab Content */}
        <TabsContent value="security">
          <div className="grid grid-cols-2 gap-4">
            <Card>
              <CardHeader>
                <h3 className="text-lg font-semibold">Security Status</h3>
              </CardHeader>
              <CardContent>
                <div className="space-y-4">
                  <div className="p-4 bg-green-50 rounded-lg border border-green-200">
                    <div className="flex items-center">
                      <Shield className="w-5 h-5 text-green-500 mr-2" />
                      <span className="font-medium text-green-700">System Protected</span>
                    </div>
                    <p className="text-sm text-green-600 mt-1">All security measures are active and up-to-date</p>
                  </div>
                  <div className="grid grid-cols-2 gap-4">
                    <div className="p-3 bg-gray-50 rounded-lg">
                      <p className="text-sm text-gray-500">Last Scan</p>
                      <p className="font-medium">2 hours ago</p>
                    </div>
                    <div className="p-3 bg-gray-50 rounded-lg">
                      <p className="text-sm text-gray-500">Threats Blocked</p>
                      <p className="font-medium">24 this week</p>
                    </div>
                  </div>
                </div>
              </CardContent>
            </Card>

            <Card>
              <CardHeader>
                <h3 className="text-lg font-semibold">Firewall Activity</h3>
              </CardHeader>
              <CardContent>
                <ResponsiveContainer width="100%" height={200}>
                  <LineChart data={[
                    {time: '12:00', blocked: 5},
                    {time: '13:00', blocked: 8},
                    {time: '14:00', blocked: 3},
                    {time: '15:00', blocked: 12}
                  ]}>
                    <CartesianGrid strokeDasharray="3 3" />
                    <XAxis dataKey="time" />
                    <YAxis />
                    <Tooltip />
                    <Line type="monotone" dataKey="blocked" stroke="#ef4444" name="Blocked Attempts" />
                  </LineChart>
                </ResponsiveContainer>
              </CardContent>
            </Card>
          </div>

          <Card className="mt-4">
            <CardHeader>
              <h3 className="text-lg font-semibold">Recent Security Events</h3>
            </CardHeader>
            <CardContent>
              <div className="space-y-3">
                {[
                  { type: 'Malware Blocked', severity: 'High', time: '15:30', source: '192.168.1.105' },
                  { type: 'Suspicious Login', severity: 'Medium', time: '14:45', source: '10.0.0.15' },
                  { type: 'Port Scan Detected', severity: 'Low', time: '13:20', source: '172.16.0.100' },
                ].map((event, i) => (
                  <div key={i} className="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                    <div>
                      <p className="font-medium">{event.type}</p>
                      <p className="text-sm text-gray-500">Source: {event.source}</p>
                    </div>
                    <div className="text-right">
                      <span className={`px-2 py-1 rounded text-sm ${
                        event.severity === 'High' ? 'bg-red-100 text-red-700' :
                        event.severity === 'Medium' ? 'bg-yellow-100 text-yellow-700' :
                        'bg-blue-100 text-blue-700'
                      }`}>
                        {event.severity}
                      </span>
                      <p className="text-sm text-gray-500 mt-1">{event.time}</p>
                    </div>
                  </div>
                ))}
              </div>
            </CardContent>
          </Card>
        </TabsContent>

        {/* Storage Tab Content */}
        <TabsContent value="storage">
          <div className="grid grid-cols-2 gap-4">
            <Card>
              <CardHeader>
                <h3 className="text-lg font-semibold">Storage Overview</h3>
              </CardHeader>
              <CardContent>
                <div className="space-y-4">
                  <div>
                    <div className="flex justify-between mb-2">
                      <span>C: Drive (System)</span>
                      <span>820 GB / 1 TB</span>
                    </div>
                    <Progress value={82} className="h-2" />
                    <div className="grid grid-cols-3 gap-2 mt-2">
                      <div className="p-2 bg-blue-50 rounded">
                        <p className="text-xs text-blue-600">System</p>
                        <p className="font-medium">250 GB</p>
                      </div>
                      <div className="p-2 bg-green-50 rounded">
                        <p className="text-xs text-green-600">Apps</p>
                        <p className="font-medium">320 GB</p>
                      </div>
                      <div className="p-2 bg-purple-50 rounded">
                        <p className="text-xs text-purple-600">Files</p>
                        <p className="font-medium">250 GB</p>
                      </div>
                    </div>
                  </div>

                  <div>
                    <div className="flex justify-between mb-2">
                      <span>D: Drive (Data)</span>
                      <span>1.2 TB / 2 TB</span>
                    </div>
                    <Progress value={60} className="h-2" />
                  </div>
                </div>
              </CardContent>
            </Card>

            <Card>
              <CardHeader>
                <h3 className="text-lg font-semibold">Disk Health</h3>
              </CardHeader>
              <CardContent>
                <div className="space-y-4">
                  <div className="p-4 bg-green-50 rounded-lg">
                    <div className="flex items-center justify-between">
                      <div>
                        <p className="font-medium text-green-700">Disk Status: Healthy</p>
                        <p className="text-sm text-green-600">All drives operating normally</p>
                      </div>
                      <HardDrive className="w-6 h-6 text-green-500" />
                    </div>
                  </div>
                  <div className="grid grid-cols-2 gap-4">
                    <div className="p-3 bg-gray-50 rounded-lg">
                      <p className="text-sm text-gray-500">Read Speed</p>
                      <p className="text-xl font-bold">520 MB/s</p>
                    </div>
                    <div className="p-3 bg-gray-50 rounded-lg">
                      <p className="text-sm text-gray-500">Write Speed</p>
                      <p className="text-xl font-bold">480 MB/s</p>
                    </div>
                  </div>
                </div>
              </CardContent>
            </Card>
          </div>

          <Card className="mt-4">
            <CardHeader>
              <h3 className="text-lg font-semibold">Large Files</h3>
            </CardHeader>
            <CardContent>
              <div className="space-y-3">
                {[
                  { name: 'Project_Backup.zip', size: '15.4 GB', location: 'D:\\Backups', modified: '2025-01-15' },
                  { name: 'VM_Image.vhdx', size: '25.8 GB', location: 'C:\\Virtual Machines', modified: '2025-01-14' },
                  { name: 'Database_Dump.sql', size: '8.2 GB', location: 'D:\\Database', modified: '2025-01-13' },
                ].map((file, i) => (
                  <div key={i} className="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                    <div>
                      <p className="font-medium">{file.name}</p>
                      <p className="text-sm text-gray-500">{file.location}</p>
                    </div>
                    <div className="text-right">
                      <p className="font-medium">{file.size}</p>
                      <p className="text-sm text-gray-500">Modified: {file.modified}</p>
                    </div>
                  </div>
                ))}
              </div>
            </CardContent>
          </Card>
        </TabsContent>
        <TabsContent value="database">
          <Card>
            <CardHeader>
              <h3 className="text-lg font-semibold">Database Status</h3>
            </CardHeader>
            <CardContent>
              <div className="space-y-4">
                <div className="grid grid-cols-2 gap-4">
                  <div className="p-4 bg-gray-50 rounded-lg">
                    <h4 className="font-medium mb-2">Active Connections</h4>
                    <p className="text-2xl font-bold text-purple-600">24</p>
                  </div>
                  <div className="p-4 bg-gray-50 rounded-lg">
                    <h4 className="font-medium mb-2">Query Response Time</h4>
                    <p className="text-2xl font-bold text-green-600">45ms</p>
                  </div>
                </div>
                <Alert>
                  <AlertTriangle className="h-4 w-4" />
                  <AlertTitle>Database Health</AlertTitle>
                  <AlertDescription>
                    All database systems are operating normally. Last backup completed successfully.
                  </AlertDescription>
                </Alert>
              </div>
            </CardContent>
          </Card>
        </TabsContent>
      </Tabs>
    </div>
  );
};

export default GuardianXDashboard;
