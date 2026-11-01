import React, { useState } from 'react';
import { 
  Filter, 
  Calendar, 
  User, 
  ChevronDown, 
  ChevronUp, 
  BellAlert, // Using Bell as alternative
  Bell,
  Megaphone, 
  Activity, 
  Clock,
  TrendingUp,
  AlertCircle,
  CheckCircle2
} from 'lucide-react';

// --- Reusable Components ---

const KPICard = ({ title, value, trend, isPositive }) => (
  <div className="bg-white p-5 rounded-xl border border-gray-100 shadow-sm flex flex-col justify-between hover:shadow-md transition-shadow">
    <h3 className="text-sm font-medium text-gray-500 mb-2">{title}</h3>
    <div className="flex items-end justify-between">
      <span className="text-2xl font-bold text-gray-800">{value}</span>
      {trend && (
        <span className={`text-xs font-semibold px-2 py-1 rounded-full ${isPositive ? 'bg-emerald-50 text-emerald-600' : 'bg-rose-50 text-rose-600'}`}>
          {isPositive ? '+' : '-'}{trend}
        </span>
      )}
    </div>
  </div>
);

const AccordionItem = ({ icon: Icon, title, content, badge }) => {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <div className="border-b border-gray-100 last:border-0">
      <button 
        onClick={() => setIsOpen(!isOpen)}
        className="w-full flex items-center justify-between py-4 text-left hover:bg-gray-50 transition-colors px-2 rounded-lg"
      >
        <div className="flex items-center gap-3">
          <div className="p-2 bg-gray-100 text-gray-600 rounded-lg">
            <Icon size={18} />
          </div>
          <span className="font-medium text-gray-700">{title}</span>
        </div>
        <div className="flex items-center gap-3">
          {badge && (
            <span className="flex h-5 w-5 items-center justify-center rounded-full bg-rose-100 text-[10px] font-bold text-rose-600">
              {badge}
            </span>
          )}
          {isOpen ? <ChevronUp size={18} className="text-gray-400" /> : <ChevronDown size={18} className="text-gray-400" />}
        </div>
      </button>
      {isOpen && (
        <div className="px-2 pb-4 pt-1 text-sm text-gray-500 leading-relaxed animate-in slide-in-from-top-2 fade-in duration-200">
          {content}
        </div>
      )}
    </div>
  );
};

// --- View Components ---

const OperationView = () => (
  <div className="space-y-6 animate-in fade-in duration-300">
    {/* KPI Grid */}
    <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
      <KPICard title="Total Produksi" value="12,450" trend="5.2%" isPositive={true} />
      <KPICard title="Efisiensi Mesin" value="94.2%" trend="1.1%" isPositive={true} />
      <KPICard title="Insiden Keselamatan" value="2" trend="1" isPositive={false} />
    </div>

    {/* Chart Mockup */}
    <div className="bg-white p-6 rounded-xl border border-gray-100 shadow-sm">
      <div className="flex items-center justify-between mb-6">
        <h3 className="font-semibold text-gray-800">Grafik Output Produksi (Mingguan)</h3>
        <select className="text-sm border-gray-200 rounded-lg text-gray-500 focus:ring-blue-500">
          <option>7 Hari Terakhir</option>
          <option>Bulan Ini</option>
        </select>
      </div>
      {/* Simple Bar Chart Mockup using Flexbox */}
      <div className="h-48 flex items-end justify-between gap-2 px-2">
        {[40, 70, 45, 90, 65, 80, 55].map((height, i) => (
          <div key={i} className="w-full bg-blue-100 rounded-t-sm relative group hover:bg-blue-200 transition-colors" style={{ height: `${height}%` }}>
            <div className="absolute -top-8 left-1/2 -translate-x-1/2 bg-gray-800 text-white text-xs px-2 py-1 rounded opacity-0 group-hover:opacity-100 transition-opacity">
              {height * 10}
            </div>
            <div className="w-full bg-blue-500 rounded-t-sm absolute bottom-0" style={{ height: `${height * 0.7}%` }}></div>
          </div>
        ))}
      </div>
      <div className="flex justify-between mt-3 text-xs text-gray-400 px-4">
        <span>Sen</span><span>Sel</span><span>Rab</span><span>Kam</span><span>Jum</span><span>Sab</span><span>Min</span>
      </div>
    </div>

    {/* Table */}
    <div className="bg-white rounded-xl border border-gray-100 shadow-sm overflow-hidden">
      <div className="p-5 border-b border-gray-100">
        <h3 className="font-semibold text-gray-800">Status Operasional Area</h3>
      </div>
      <div className="overflow-x-auto">
        <table className="w-full text-left text-sm">
          <thead className="bg-gray-50/50 text-gray-500 border-b border-gray-100">
            <tr>
              <th className="font-medium p-4">Area</th>
              <th className="font-medium p-4">Status</th>
              <th className="font-medium p-4">Update Terakhir</th>
              <th className="font-medium p-4">Penanggung Jawab</th>
            </tr>
          </thead>
          <tbody className="divide-y divide-gray-50">
            <tr className="hover:bg-gray-50/50 transition-colors">
              <td className="p-4 font-medium text-gray-700">Area Perakitan A</td>
              <td className="p-4">
                <span className="inline-flex items-center gap-1.5 py-1 px-2.5 rounded-full text-xs font-medium bg-emerald-50 text-emerald-700">
                  <CheckCircle2 size={14} /> Normal
                </span>
              </td>
              <td className="p-4 text-gray-500">10:45 AM</td>
              <td className="p-4 text-gray-600">Budi Santoso</td>
            </tr>
            <tr className="hover:bg-gray-50/50 transition-colors">
              <td className="p-4 font-medium text-gray-700">Gudang Bahan Baku</td>
              <td className="p-4">
                <span className="inline-flex items-center gap-1.5 py-1 px-2.5 rounded-full text-xs font-medium bg-amber-50 text-amber-700">
                  <AlertCircle size={14} /> Menipis
                </span>
              </td>
              <td className="p-4 text-gray-500">09:15 AM</td>
              <td className="p-4 text-gray-600">Siti Aminah</td>
            </tr>
            <tr className="hover:bg-gray-50/50 transition-colors">
              <td className="p-4 font-medium text-gray-700">Distribusi Utama</td>
              <td className="p-4">
                <span className="inline-flex items-center gap-1.5 py-1 px-2.5 rounded-full text-xs font-medium bg-emerald-50 text-emerald-700">
                  <CheckCircle2 size={14} /> Normal
                </span>
              </td>
              <td className="p-4 text-gray-500">Kemarin, 16:00</td>
              <td className="p-4 text-gray-600">Reza Pahlevi</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
);

const BusinessDevView = () => (
  <div className="space-y-6 animate-in fade-in duration-300">
    {/* KPI Grid */}
    <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
      <KPICard title="Total Klien Aktif" value="6" trend="0" isPositive={true} />
      <KPICard title="Potensi Pendapatan" value="Rp 5.5M" trend="2.4%" isPositive={true} />
      <KPICard title="Prospek Hilang" value="8" trend="8" isPositive={false} />
    </div>

    {/* Pipeline Chart Mockup */}
    <div className="bg-white p-6 rounded-xl border border-gray-100 shadow-sm">
      <h3 className="font-semibold text-gray-800 mb-6">Sales Pipeline</h3>
      {/* Simple Funnel/Pipeline Mockup */}
      <div className="flex flex-col md:flex-row gap-4 justify-between items-center mb-4">
        {[
          { step: 'Leads', val: '15', color: 'bg-slate-100', border: 'border-slate-300' },
          { step: 'Kontak Awal', val: '7', color: 'bg-blue-50', border: 'border-blue-200' },
          { step: 'Proposal', val: '15', color: 'bg-indigo-50', border: 'border-indigo-200' },
          { step: 'Negosiasi', val: '14', color: 'bg-purple-50', border: 'border-purple-200' },
          { step: 'Goal (Closed)', val: '6', color: 'bg-emerald-50', border: 'border-emerald-200' },
        ].map((item, index) => (
          <React.Fragment key={index}>
            <div className={`flex-1 w-full flex flex-col items-center justify-center p-4 rounded-xl border-2 ${item.border} ${item.color}`}>
              <span className="text-2xl font-bold text-gray-800 mb-1">{item.val}</span>
              <span className="text-xs font-medium text-gray-500 uppercase tracking-wider">{item.step}</span>
            </div>
            {index < 4 && (
              <div className="hidden md:block text-gray-300">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="m9 18 6-6-6-6"/></svg>
              </div>
            )}
          </React.Fragment>
        ))}
      </div>
    </div>

    {/* Table */}
    <div className="bg-white rounded-xl border border-gray-100 shadow-sm overflow-hidden">
      <div className="p-5 border-b border-gray-100 flex justify-between items-center">
        <h3 className="font-semibold text-gray-800">Daftar Prospek Prioritas</h3>
        <button className="text-sm text-blue-600 font-medium hover:text-blue-700">Lihat Semua</button>
      </div>
      <div className="overflow-x-auto">
        <table className="w-full text-left text-sm">
          <thead className="bg-gray-50/50 text-gray-500 border-b border-gray-100">
            <tr>
              <th className="font-medium p-4">Nama Perusahaan</th>
              <th className="font-medium p-4">Tahapan</th>
              <th className="font-medium p-4">Estimasi Nilai</th>
              <th className="font-medium p-4">Action</th>
            </tr>
          </thead>
          <tbody className="divide-y divide-gray-50">
            {[
              { name: 'PT IKPT', stage: 'Negosiasi', val: 'Rp 1.2M', tag: 'bg-purple-100 text-purple-700' },
              { name: 'PT REKIND', stage: 'Proposal', val: 'Rp 450Jt', tag: 'bg-indigo-100 text-indigo-700' },
              { name: 'PT REKIND', stage: 'Kontak Awal', val: 'Rp 2.1M', tag: 'bg-blue-100 text-blue-700' },
            ].map((row, i) => (
              <tr key={i} className="hover:bg-gray-50/50 transition-colors">
                <td className="p-4 font-medium text-gray-700">{row.name}</td>
                <td className="p-4">
                  <span className={`inline-flex items-center py-1 px-2.5 rounded-full text-xs font-medium ${row.tag}`}>
                    {row.stage}
                  </span>
                </td>
                <td className="p-4 text-gray-600 font-medium">{row.val}</td>
                <td className="p-4">
                  <button className="text-gray-400 hover:text-blue-600 transition-colors">
                    <TrendingUp size={18} />
                  </button>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  </div>
);

// --- Main App Component ---

export default function App() {
  const [activeTab, setActiveTab] = useState('operation');

  return (
    <div className="min-h-screen bg-slate-50 text-slate-800 font-sans selection:bg-blue-100">
      {/* Header */}
      <header className="bg-white border-b border-gray-200 sticky top-0 z-10">
        <div className="max-w-[1400px] mx-auto px-6 h-16 flex items-center justify-between">
          <div className="flex items-center gap-3">
            <div className="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center shadow-inner">
              <span className="text-white font-bold text-lg leading-none">C</span>
            </div>
            <h1 className="font-bold text-lg tracking-tight text-gray-900 hidden sm:block">
              PT CODA INTEGRA INTERNUSA
            </h1>
          </div>
          
          <div className="flex items-center gap-3 md:gap-4">
            <button className="flex items-center gap-2 px-3 py-1.5 text-sm font-medium text-gray-600 hover:bg-gray-100 rounded-md transition-colors border border-gray-200">
              <Filter size={16} />
              <span className="hidden md:inline">Filter</span>
            </button>
            <div className="relative hidden sm:block">
              <input 
                type="date" 
                className="pl-9 pr-3 py-1.5 text-sm font-medium text-gray-600 border border-gray-200 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500/20 focus:border-blue-500"
                defaultValue={new Date().toISOString().split('T')[0]}
              />
              <Calendar size={16} className="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400 pointer-events-none" />
            </div>
            <div className="h-6 w-px bg-gray-200 mx-1 hidden md:block"></div>
            <button className="flex items-center justify-center w-9 h-9 bg-gray-100 text-gray-600 hover:bg-blue-50 hover:text-blue-600 rounded-full transition-colors">
              <User size={18} />
            </button>
          </div>
        </div>
      </header>

      {/* Main Content Layout */}
      <main className="max-w-[1400px] mx-auto px-6 py-8">
        <div className="flex flex-col lg:flex-row gap-8">
          
          {/* Left Column (Main Area) */}
          <div className="flex-1 lg:max-w-[calc(100%-320px)] xl:max-w-[calc(100%-380px)]">
            
            {/* Custom Tabs */}
            <div className="flex space-x-1 bg-gray-100/80 p-1 rounded-xl w-fit mb-8 border border-gray-200/50">
              <button
                onClick={() => setActiveTab('operation')}
                className={`px-6 py-2.5 text-sm font-semibold rounded-lg transition-all duration-200 ${
                  activeTab === 'operation' 
                    ? 'bg-white text-blue-700 shadow-sm' 
                    : 'text-gray-500 hover:text-gray-700 hover:bg-gray-200/50'
                }`}
              >
                OPERATION
              </button>
              <button
                onClick={() => setActiveTab('business')}
                className={`px-6 py-2.5 text-sm font-semibold rounded-lg transition-all duration-200 ${
                  activeTab === 'business' 
                    ? 'bg-white text-blue-700 shadow-sm' 
                    : 'text-gray-500 hover:text-gray-700 hover:bg-gray-200/50'
                }`}
              >
                BUSINESS DEV
              </button>
            </div>

            {/* Dynamic View based on Tab */}
            {activeTab === 'operation' ? <OperationView /> : <BusinessDevView />}
            
          </div>

          {/* Right Column (Sidebar) */}
          <aside className="w-full lg:w-[300px] xl:w-[340px] shrink-0">
            <div className="bg-white rounded-xl border border-gray-100 shadow-sm p-5 sticky top-24">
              <h2 className="text-sm font-bold text-gray-800 uppercase tracking-wider mb-4 px-2">Info Terkini</h2>
              
              <div className="flex flex-col">
                <AccordionItem 
                  icon={Bell} 
                  title="Alert" 
                  badge="2"
                  content={
                    <ul className="space-y-3">
                      <li className="flex gap-2">
                        <span className="w-1.5 h-1.5 rounded-full bg-rose-500 mt-1.5 shrink-0"></span>
                        <span>Keterlambatan pengiriman qtn dari Vendor A.</span>
                      </li>
                      <li className="flex gap-2">
                        <span className="w-1.5 h-1.5 rounded-full bg-amber-500 mt-1.5 shrink-0"></span>
                        <span>Keterlambatan pengiriman material dari Vendor B.</span>
                      </li>
                    </ul>
                  } 
                />
                <AccordionItem 
                  icon={Megaphone} 
                  title="Pengumuman" 
                  content="Meeting Clarification Technical akan diadakan pada hari Senin 2 oct 26, pukul 8:00 WIB di Ruang Utama Rekind." 
                />
                <AccordionItem 
                  icon={Activity} 
                  title="Aktivitas Terbaru" 
                  content={
                    <ul className="space-y-2 text-xs">
                      <li>• User Admin mengupdate target KPI (1 jam lalu)</li>
                      <li>• Laporan harian shift malam diunggah (4 jam lalu)</li>
                      <li>• Klien baru 'PT Maju Bersama' ditambahkan (Kemarin)</li>
                    </ul>
                  } 
                />
                <AccordionItem 
                  icon={Clock} 
                  title="Update Terakhir" 
                  content="Sistem terakhir kali disinkronisasi pada: 31 Okt 2026, 09:15 AM WIB. Semua data up-to-date." 
                />
              </div>
            </div>
          </aside>

        </div>
      </main>
    </div>
  );
}
