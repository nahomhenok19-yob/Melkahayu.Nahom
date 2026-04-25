# Melkahayu.Nahom
Social media application 
Nahi12:
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title>melkahayu.nahom</title>
  </head>
  <body class="bg-black">
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>

import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&family=Playfair+Display:ital,wght@0,700;0,900;1,700;1,900&family=JetBrains+Mono:wght@400;700&display=swap');
@import "tailwindcss";

@theme {
  --font-sans: "Inter", ui-sans-serif, system-ui, sans-serif;
  --font-serif: "Playfair Display", ui-serif, Georgia, serif;
  --font-mono: "JetBrains Mono", ui-monospace, SFMono-Regular, monospace;
  
  --color-black-pure: #000000;
  --color-black-soft: #0A0A0A;
  --color-gold: #D4AF37;
  --color-gold-light: #F9E27D;
  --color-gold-dark: #B8860B;
}

@layer base {
  body {
    @apply font-sans;
    -webkit-tap-highlight-color: transparent;
  }
}

@layer components {
  .gold-gradient {
    background: linear-gradient(135deg, #B8860B 0%, #D4AF37 50%, #F9E27D 100%);
  }

  .vip-shine {
    position: relative;
    overflow: hidden;
  }

  .vip-shine::after {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background: linear-gradient(
      transparent,
      rgba(255, 255, 255, 0.3),
      transparent
    );
    transform: rotate(45deg);
    animation: shine 3s infinite;
  }

  .golden-emoji {
    filter: drop-shadow(0 0 8px rgba(212, 175, 55, 0.5));
  }
}

@keyframes shine {
  0% { transform: translateX(-100%) rotate(45deg); }
  100% { transform: translateX(100%) rotate(45deg); }
}

.no-scrollbar::-webkit-scrollbar {
  display: none;
}
.no-scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}

/* Custom transitions */
.page-transition-enter {
  opacity: 0;
  transform: translateY(10px);
}
.page-transition-enter-active {
  opacity: 1;
  transform: translateY(0);
  transition: opacity 300ms, transform 300ms;
}

import { Timestamp } from 'firebase/firestore';

export interface UserProfile {
  uid: string;
  email: string;
  displayName: string;
  photoURL: string;
  bio?: string;
  coins: number;
  isVip: boolean;
  vipExpiry?: Timestamp;
  role: 'user' | 'admin' | 'owner';
  followersCount: number;
  followingCount: number;
  createdAt: Timestamp;
  lastMoodUpdate?: Timestamp;
  currentMood?: string;
  totalGiftsReceived?: number;
}

export interface Post {
  id: string;
  authorId: string;
  type: 'text' | 'image' | 'video' | 'audio';
  content: string;
  caption?: string;
  likes: number;
  views: number;
  commentsCount: number;
  createdAt: Timestamp;
  filter?: string;
  seenBy?: string[];
}

export interface MoodPost {
  id: string;
  userId: string;
  mood: string;
  text: string;
  isAnonymous: boolean;
  reactions: {
    heart: number;
    hug: number;
    thumb: number;
  };
  createdAt: Timestamp;
  seenBy?: string[];
}

export interface Land {
  id: string;
  name: string;
  description: string;
  type: 'education' | 'equb' | 'edir' | 'ministry';
  ownerId: string;
  members: string[];
  createdAt: Timestamp;
  equbAmount?: number;
  equbCycle?: string;
}

export interface ChatMessage {
  id: string;
  senderId: string;
  senderName: string;
  senderPhoto: string;
  text: string;
  createdAt: Timestamp;
}

export interface Gift {
  id: string;
  name: string;
  price: number;
  icon: string;
}

export interface LuxuryAsset {
  id: string;
  name: string;
  description: string;
  image: string;
  price: number;
  ownerId: string;
  rarity: 'rare' | 'epic' | 'legendary';
}

{
  "name": "melkahayu-nahom",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
  "dependencies": {
    "firebase": "^10.8.0",
    "framer-motion": "^11.0.5",
    "lucide-react": "^0.344.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "clsx": "^2.1.0",
    "tailwind-merge": "^2.2.1",
    "canvas-confetti": "^1.9.2"
  },
  "devDependencies": {
    "@types/react": "^18.2.56",
    "@types/react-dom": "^18.2.19",
    "@types/canvas-confetti": "^1.6.4",
    "@vitejs/plugin-react": "^4.2.1",
    "autoprefixer": "^10.4.17",
    "postcss": "^8.4.35",
    "tailwindcss": "^3.4.1",
    "typescript": "^5.2.2",
    "vite": "^5.1.4"
  }
}

import React, { useState, useEffect, useRef } from 'react';
import { 
  Home, Search, PlusSquare, Heart, User, Settings, 
  Coins, Trophy, ShieldCheck, Crown, Gift as GiftIcon,
  MessageCircle, Send, Share2, Eye, Map, BookOpen,
  Users, Landmark, Music, Play, Pause, Camera,
  MoreVertical, Bell, Star, AlertTriangle, Phone,
  Mic, Video, MapPin, HandMetal, Smartphone,
  Fingerprint, ScanFace, LogOut
} from 'lucide-react';
import { motion, AnimatePresence } from 'framer-motion';
import { initializeApp } from 'firebase/app';
import { 
  getAuth, signInWithPopup, GoogleAuthProvider, 
  onAuthStateChanged, User as FirebaseUser 
} from 'firebase/auth';
import { 
  getFirestore, collection, doc, setDoc, getDoc, 
  onSnapshot, query, orderBy, limit, where,
  updateDoc, increment, arrayUnion, Timestamp,
  addDoc, deleteDoc, serverTimestamp
} from 'firebase/firestore';
import confetti from 'canvas-confetti';
import firebaseConfig from '../firebase-applet-config.json';
import { 
  UserProfile, Post, MoodPost, Land, 
  ChatMessage, Gift, LuxuryAsset 
} from './types';

// Initialize Firebase
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

// ... (Rest of the 5,000+ lines of App.tsx logic)

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title>melkahayu.nahom - Luxury Social</title>
    <style>
      body {
        margin: 0;
        background-color: #000;
        color: #fff;
        overflow: hidden;
      }
      #root {
        height: 100vh;
        width: 100vw;
      }
    </style>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>

{
  "name": "melkahayu-nahom-luxury",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
  "dependencies": {
    "@google/genai": "^0.21.0",
    "canvas-confetti": "^1.9.3",
    "clsx": "^2.1.1",
    "firebase": "^11.0.1",
    "framer-motion": "^11.11.11",
    "lucide-react": "^0.454.0",
    "react": "^18.3.1",
    "react-dom": "^18.3.1",
    "react-markdown": "^9.0.1",
    "tailwind-merge": "^2.5.4"
  },
  "devDependencies": {
    "@types/canvas-confetti": "^1.6.4",
    "@types/react": "^18.3.12",
    "@types/react-dom": "^18.3.1",
    "@vitejs/plugin-react": "^4.3.3",
    "autoprefixer": "^10.4.20",
    "postcss": "^8.4.47",
    "tailwindcss": "^3.4.14",
    "typescript": "^5.6.3",
    "vite": "^5.4.10"
  }
}

import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.tsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)

@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400..900;1,400..900&family=Inter:wght@100..900&display=swap');

@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  background-color: #000;
}

body {
  font-family: 'Inter', sans-serif;
  background-color: #000;
  -webkit-tap-highlight-color: transparent;
}

.font-serif {
  font-family: 'Playfair Display', serif;
}

.gold-gradient {
  background: linear-gradient(135deg, #D4AF37 0%, #F9E27D 50%, #D4AF37 100%);
}

.vip-shine {
  box-shadow: 0 0 15px rgba(212, 175, 55, 0.4);
  animation: shine 3s infinite;
}

@keyframes shine {
  0% { filter: brightness(1); }
  50% { filter: brightness(1.3); }
  100% { filter: brightness(1); }
}

.golden-emoji {
  filter: drop-shadow(0 0 10px rgba(212, 175, 55, 0.8));
}

.no-scrollbar::-webkit-scrollbar {
  display: none;
}
.no-scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.bg-black-pure { background-color: #000000; }
.bg-black-soft { background-color: #0a0a0a; }
.text-gold { color: #D4AF37; }
.border-gold { border-color: #D4AF37; }

import { Timestamp } from 'firebase/firestore';

export interface UserProfile {
  uid: string;
  displayName: string;
  email: string;
  photoURL: string;
  bio?: string;
  coins: number;
  isVip: boolean;
  vipExpiry?: Timestamp | null;
  role: 'owner' | 'admin' | 'user';
  followersCount: number;
  followingCount: number;
  totalGiftsReceived: number;
  currentMood?: string;
  lastMoodUpdate?: Timestamp;
}

export interface Post {
  id: string;
  authorId: string;
  type: 'text' | 'image' | 'video' | 'audio';
  content: string;
  caption?: string;
  likes: number;
  commentsCount: number;
  views: number;
  createdAt: Timestamp;
  seenBy?: string[];
  filter?: string;
}

export interface MoodPost {
  id: string;
  userId: string;
  mood: string;
  text: string;
  reactions: {
    heart: number;
    hug: number;
    thumb: number;
  };
  isAnonymous: boolean;
  createdAt: Timestamp;
  seenBy?: string[];
}

export interface Land {
  id: string;
  name: string;
  description: string;
  type: 'education' | 'equb' | 'edir' | 'ministry';
  ownerId: string;
  members: string[];
  createdAt: Timestamp;
  equbAmount?: number;
  equbCycle?: 'daily' | 'weekly' | 'monthly';
}

export interface Message {
  id: string;
  senderId: string;
  senderName: string;
  senderPhoto: string;
  text: string;
  createdAt: Timestamp;
}

export interface Gift {
  id: string;
  name: string;
  price: number;
  icon: string;
}

import React, { useState, useEffect, useRef } from 'react';
import { 
  motion, 
  AnimatePresence 
} from 'motion/react';
import { 
  initializeFirebase, 
  auth as ig, 
  db as rt, 
  GoogleAuthProvider, 
  signInWithPopup,
  onAuthStateChanged,
  doc,
  setDoc,
  getDoc,
  updateDoc,
  collection,
  addDoc,
  onSnapshot,
  query,
  orderBy,
  limit,
  where,
  increment,
  arrayUnion,
  deleteDoc,
  getDocs,
  serverTimestamp as Ar
} from './lib/firebase';
import { 
  Search, 
  Plus, 
  Home, 
  MessageCircle, 
  User, 
  Heart, 
  Share2, 
  Coins, 
  ShieldCheck, 
  Crown, 
  Gift, 
  Zap, 
  Eye, 
  CheckCircle2, 
  LogOut, 
  Settings, 
  MapPin, 
  PhoneCall, 
  Video, 
  Scan, 
  Bell, 
  Trophy, 
  Sparkles, 
  Globe, 
  Lock, 
  Mic, 
  MoreHorizontal, 
  Filter, 
  X,
  Play,
  Pause,
  Volume2,
  VolumeX,
  Send,
  Trash2,
  Camera,
  Layers,
  Diamond,
  Compass,
  AlertTriangle,
  History,
  LifeBuoy,
  HelpCircle,
  Sticker,
  Smile,
  Image as ImageIcon,
  Flag,
  UserPlus,
  UserMinus,
  MessageSquare,
  Hash,
  Star,
  ZapOff,
  Database,
  Briefcase,
  GraduationCap,
  Scale,
  Church,
  Mic2,
  Music,
  Map as MapIcon,
  ChevronRight,
  TrendingUp,
  Award,
  DollarSign
} from 'lucide-react';
import { clsx, type ClassValue } from 'clsx';
import { twMerge } from 'tailwind-merge';

// Utility for Tailwind classes
function yn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}

// Types
interface UserProfile {
  uid: string;
  displayName: string;
  email: string;
  photoURL: string;
  isVip: boolean;
  vipExpiry?: any;
  coins: number;
  followersCount: number;
  followingCount: number;
  bio: string;
  role: 'owner' | 'admin' | 'user';
  currentMood?: string;
  lastMoodUpdate?: any;
  isVerified: boolean;
  createdAt: any;
  totalGiftsReceived: number;
}

interface Post {
  id: string;
  authorId: string;
  authorName: string;
  authorPhoto: string;
  text: string;
  mediaUrl?: string;
  mediaType: 'image' | 'video' | 'text' | 'audio';
  likes: number;
  commentsCount: number;
  shares: number;
  views: number;
  seenBy: string[];
  createdAt: any;
  mood?: string;
  filter?: string;
}

interface MoodPost {
  id: string;
  userId: string;
  mood: string;
  text: string;
  reactions: {
    heart: number;
    hug: number;
    thumb: number;
  };
  createdAt: any;
  isAnonymous: boolean;
  seenBy: string[];
}

interface Message {
  id: string;
  senderId: string;
  senderName: string;
  senderPhoto: string;
  text: string;
  createdAt: any;
  type: 'text' | 'image' | 'system';
}

interface Land {
  id: string;
  name: string;
  description: string;
  type: 'education' | 'equb' | 'edir' | 'ministry';
  ownerId: string;
  members: string[];
  createdAt: any;
  image?: string;
  amount?: number;
  cycle?: string;
}

interface Gift {
  id: string;
  name: string;
  price: number;
  icon: string;
}

// Mood Mapping
const Rh: Record<string, string> = {
  Happy: "😊",
  Sad: "😔",
  Angry: "😠",
  Loved: "🥰",
  Bored: "😑",
  Excited: "🤩",
  Tired: "😴",
  Calm: "😌",
  Lonely: "🥺"
};

// Filters Mapping
const FILTERS: Record<string, string> = {
  none: '',
  luxury: 'sepia(0.3) contrast(1.1) brightness(1.1) saturate(1.2)',
  vintage: 'grayscale(0.2) sepia(0.5) contrast(0.9)',
  neon: 'hue-rotate(290deg) saturate(1.5)',
  midnight: 'brightness(0.7) contrast(1.2) saturate(0.5) hue-rotate(200deg)',
  ethiopian: 'sepia(0.2) saturate(1.3) contrast(1.05) brightness(1.02)'
};

export default function App() {
  // Auth State
  const [user, setUser] = useState<any>(null);
  const [profile, setProfile] = useState<UserProfile | null>(null);
  const [loading, setLoading] = useState(true);

  // Navigation State
  const [activeTab, setActiveTab] = useState('home');
  const [homeSubTab, setHomeSubTab] = useState<'moods' | 'videos' | 'offline'>('moods');
  const [viewingProfileId, setViewingProfileId] = useState<string | null>(null);
  const [isVipModalOpen, setIsVipModalOpen] = useState(false);
  const [selectedPlan, setSelectedPlan] = useState('monthly');
  const [isGiftShopOpen, setIsGiftShopOpen] = useState(false);
  const [selectedRecipientId, setSelectedRecipientId] = useState<string | null>(null);

  // Data State
  const [posts, setPosts] = useState<Post[]>([]);
  const [moodPosts, setMoodPosts] = useState<MoodPost[]>([]);
  const [lands, setLands] = useState<Land[]>([]);
  const [messages, setMessages] = useState<Message[]>([]);
  const [activeChatId, setActiveChatId] = useState<string | null>(null);
  const [allUsers, setAllUsers] = useState<UserProfile[]>([]);
  const [following, setFollowing] = useState<string[]>([]);
  
  // Interaction State
  const [isMatching, setIsMatching] = useState(false);
  const [matchResult, setMatchResult] = useState<any>(null);
  const [searchQuery, setSearchQuery] = useState('');
  const [showFakeCall, setShowFakeCall] = useState(false);
  const [fakeCallName, setFakeCallName] = useState('Mom');
  const [fakeCallNumber, setFakeCallNumber] = useState('+251 911 000 000');
  const [fakeCallTime, setFakeCallTime] = useState('00:00');
  const [isFakeCallActive, setIsFakeCallActive] = useState(false);
  const [fakeCallIncoming, setFakeCallIncoming] = useState(false);

  // TOASTS
  const [toasts, setToasts] = useState<{id: number, title: string, text: string, type: string}[]>([]);

  // Refs
  const scrollRef = useRef<HTMLDivElement>(null);

useEffect(() => {
    const unsubscribe = onAuthStateChanged(ig, async (u) => {
      if (u) {
        setUser(u);
        const docRef = doc(rt, 'users', u.uid);
        const docSnap = await getDoc(docRef);
        
        if (docSnap.exists()) {
          setProfile(docSnap.data() as UserProfile);
        } else {
          const newProfile: UserProfile = {
            uid: u.uid,
            displayName: u.displayName || 'Luxury Member',
            email: u.email || '',
            photoURL: u.photoURL || https://api.dicebear.com/7.x/avataaars/svg?seed=${u.uid},
            isVip: false,
            coins: 100,
            followersCount: 0,
            followingCount: 0,
            bio: 'Elite member of melkahayu.nahom',
            role: 'user',
            isVerified: false,
            createdAt: Ar(),
            totalGiftsReceived: 0
          };
          await setDoc(docRef, newProfile);
          setProfile(newProfile);
        }
      } else {
        setUser(null);
        setProfile(null);
      }
      setLoading(false);
    });

    return () => unsubscribe();
  }, []);

  // Real-time listeners
  useEffect(() => {
    if (!user) return;

    // Listen to Posts
    const postsQuery = query(collection(rt, 'posts'), orderBy('createdAt', 'desc'), limit(50));
    const unsubPosts = onSnapshot(postsQuery, (snap) => {
      setPosts(snap.docs.map(d => ({ id: d.id, ...d.data() } as Post)));
    });

    // Listen to Mood Posts
    const moodQuery = query(collection(rt, 'mood_posts'), orderBy('createdAt', 'desc'), limit(50));
    const unsubMoods = onSnapshot(moodQuery, (snap) => {
      setMoodPosts(snap.docs.map(d => ({ id: d.id, ...d.data() } as MoodPost)));
    });

    // Listen to Lands
    const landsQuery = query(collection(rt, 'lands'), orderBy('createdAt', 'desc'));
    const unsubLands = onSnapshot(landsQuery, (snap) => {
      setLands(snap.docs.map(d => ({ id: d.id, ...d.data() } as Land)));
    });

    // Listen to All Users
    const usersQuery = query(collection(rt, 'users'), limit(50));
    const unsubUsers = onSnapshot(usersQuery, (snap) => {
      setAllUsers(snap.docs.map(d => d.data() as UserProfile));
    });

    return () => {
      unsubPosts();
      unsubMoods();
      unsubLands();
      unsubUsers();
    };
  }, [user]);

  const addToast = (title: string, text: string, type: string = 'info') => {
    const id = Date.now();
    setToasts(prev => [...prev, { id, title, text, type }]);
    setTimeout(() => {
      setToasts(prev => prev.filter(t => t.id !== id));
    }, 4000);
  };

  const signIn = async () => {
    try {
      const provider = new GoogleAuthProvider();
      await signInWithPopup(ig, provider);
    } catch (error) {
      console.error(error);
      addToast("Login failed", "Please check your internet connection.", "error");
    }
  };

  const handleCreatePost = async (text: string, mediaUrl: string, mediaType: any, filter: string) => {
    if (!user) return;
    try {
      await addDoc(collection(rt, 'posts'), {
        authorId: user.uid,
        authorName: profile?.displayName || 'User',
        authorPhoto: profile?.photoURL || '',
        text,
        mediaUrl,
        mediaType,
        likes: 0,
        commentsCount: 0,
        shares: 0,
        views: 0,
        seenBy: [],
        createdAt: Ar(),
        filter
      });
      addToast("ጥረት ያድርጉ", "ተለጠፈ! ✨", "success");
    } catch (e) {
      addToast("ስህተት", "እባክዎ እንደገና ይሞክሩ።", "error");
    }
  };

  // UI Components
  const TabButton = ({ id, icon: Icon, label }: { id: string, icon: any, label: string }) => (
    <button 
      onClick={() => setActiveTab(id)}
      className={yn(
        "flex flex-col items-center gap-1 p-2 transition-all duration-300",
        activeTab === id ? "text-gold scale-110" : "text-gray-500 hover:text-white"
      )}
    >
      <Icon className={yn("w-6 h-6", activeTab === id && "shadow-[0_0_15px_rgba(212,175,55,0.5)]")} />
      <span className="text-[10px] font-bold uppercase tracking-widest">{label}</span>
    </button>
  );

if (loading) {
    return (
      <div className="h-screen w-full flex flex-col items-center justify-center bg-black-pure text-gold">
        <motion.div 
          animate={{ rotate: 360 }}
          transition={{ duration: 2, repeat: Infinity, ease: "linear" }}
          className="w-16 h-16 border-4 border-gold/20 border-t-gold rounded-full mb-4 shadow-[0_0_30px_rgba(212,175,55,0.2)]"
        />
        <p className="text-sm font-bold uppercase tracking-[0.5em] animate-pulse">melkahayu.nahom</p>
      </div>
    );
  }

  if (!user) {
    return (
      <div className="h-screen w-full bg-black-pure flex flex-col items-center justify-center p-8 overflow-hidden relative">
        {/* Background Elements */}
        <div className="absolute top-0 left-0 w-full h-full overflow-hidden pointer-events-none opacity-20">
          <div className="absolute top-1/4 -left-1/4 w-96 h-96 bg-gold/30 rounded-full blur-[120px]" />
          <div className="absolute bottom-1/4 -right-1/4 w-96 h-96 bg-gold/20 rounded-full blur-[120px]" />
        </div>
        
        <motion.div 
          initial={{ opacity: 0, y: 20 }}
          animate={{ opacity: 1, y: 0 }}
          className="text-center z-10 w-full max-w-md"
        >
          <div className="w-32 h-32 mx-auto mb-8 relative">
            <motion.div 
              animate={{ rotate: [0, 10, -10, 0] }}
              transition={{ repeat: Infinity, duration: 4 }}
              className="w-full h-full rounded-2xl bg-gradient-to-br from-gold to-gold-dark p-0.5 shadow-[0_0_50px_rgba(212,175,55,0.3)]"
            >
              <div className="w-full h-full bg-black rounded-2xl flex items-center justify-center p-4">
                <img src="input_file_1.png" alt="Logo" className="w-full h-full object-contain" referrerPolicy="no-referrer" />
              </div>
            </motion.div>
          </div>
          
          <h1 className="text-5xl font-bold mb-4 gold-gradient bg-clip-text text-transparent italic font-serif">melkahayu.nahom</h1>
          <p className="text-gray-500 mb-12 uppercase tracking-[0.4em] text-xs font-medium">Excellence in Connection</p>
          
          <button 
            onClick={signIn}
            className="w-full py-4 bg-gold text-black font-bold rounded-2xl hover:bg-gold-light transition-all transform hover:scale-[1.02] active:scale-[0.98] shadow-[0_0_30px_rgba(212,175,55,0.4)] flex items-center justify-center gap-3"
          >
            <Globe className="w-5 h-5" />
            Continue with Google
          </button>
          
          <p className="text-[10px] text-gray-600 mt-12 px-8">
            By continuing, you enter a sphere of luxury and connection. melkahayu.nahom ensures your safety and elegance.
          </p>
        </motion.div>
      </div>
    );
  }

  return (
    <div className="h-screen w-full bg-black-pure text-white flex flex-col overflow-hidden font-sans selection:bg-gold selection:text-black">
      {/* HEADER */}
      <header className="p-4 flex justify-between items-center bg-black-soft/80 backdrop-blur-md border-b border-gold/10 z-50">
        <div className="flex items-center gap-2">
           <div className="w-10 h-10 rounded-xl overflow-hidden border border-gold/30 shadow-[0_0_15px_rgba(212,175,55,0.1)]">
             <img src="input_file_1.png" alt="Logo" className="w-full h-full object-cover scale-[1.3]" />
           </div>
           <div className="hidden sm:block">
             <h1 className="text-sm font-bold gold-gradient bg-clip-text text-transparent italic">melkahayu.nahom</h1>
           </div>
        </div>

        <div className="flex items-center gap-4">
          <div className="flex items-center gap-1.5 bg-gold/10 px-3 py-1 rounded-full border border-gold/30">
            <Coins className="w-4 h-4 text-gold" />

<span className="text-gold font-bold text-xs uppercase tracking-tighter">{profile?.coins || 0} ብር</span>
          </div>
          {profile?.isVip && <Crown className="w-5 h-5 text-gold animate-bounce" />}
          <div className="w-10 h-10 rounded-full border-2 border-gold/50 overflow-hidden cursor-pointer hover:border-gold transition-all" onClick={() => { setViewingProfileId(null); setActiveTab('profile'); }}>
            <img src={profile?.photoURL} alt="Profile" className="w-full h-full object-cover" />
          </div>
        </div>
      </header>

      {/* MAIN CONTENT */}
      <main className="flex-1 overflow-y-auto no-scrollbar pb-24">
        {activeTab === 'home' && (
          <div className="flex flex-col h-full">
             {/* Sub Tabs */}
             <div className="sticky top-0 z-30 bg-black/80 backdrop-blur-md p-4 flex justify-center gap-8 border-b border-white/5">
                {['moods', 'videos', 'offline'].map((tab: any) => (
                  <button 
                    key={tab}
                    onClick={() => setHomeSubTab(tab)}
                    className={yn(
                      "text-[10px] font-bold uppercase tracking-[0.2em] relative py-1",
                      homeSubTab === tab ? "text-gold" : "text-gray-500"
                    )}
                  >
                    {tab}
                    {homeSubTab === tab && (
                      <motion.div layoutId="subTab" className="absolute -bottom-1 left-0 right-0 h-0.5 bg-gold rounded-full shadow-[0_0_10px_#D4AF37]" />
                    )}
                  </button>
                ))}
             </div>

             <div className="flex-1">
                {homeSubTab === 'moods' && (
                  <div className="p-4 space-y-6 max-w-lg mx-auto">
                    {/* Mood Matcher Banner */}
                    <div className="bg-gradient-to-r from-gold/20 via-purple-500/10 to-gold/20 p-6 rounded-[2rem] border border-gold/30 text-center relative overflow-hidden group">
                      <div className="relative z-10">
                        <Sparkles className="w-8 h-8 text-gold mx-auto mb-3 animate-pulse" />
                        <h2 className="text-xl font-bold mb-1">AI Mood Matcher</h2>
                        <p className="text-xs text-gray-400 mb-6">Find someone who feels exactly like you right now.</p>
                        <button className="px-8 py-3 bg-gold text-black font-black uppercase text-[10px] tracking-widest rounded-full hover:bg-gold-light transition-all shadow-[0_0_20px_rgba(212,175,55,0.3)]">
                          Start Matching
                        </button>
                      </div>
                      <div className="absolute top-0 right-0 w-32 h-32 bg-gold/10 rounded-full blur-3xl -mr-16 -mt-16 group-hover:bg-gold/20 transition-all duration-500" />
                    </div>

                    {/* Mood posts loop */}
                    {moodPosts.map(mp => (
                      <div key={mp.id} className="bg-black-soft border border-white/5 p-6 rounded-[2rem] hover:border-gold/20 transition-all">
                        <div className="flex items-center gap-3 mb-4">
                           <div className="w-10 h-10 rounded-full bg-gold/10 flex items-center justify-center text-xl">
                             {Rh[mp.mood] || '✨'}
                           </div>
                           <div>
                             <p className="font-bold text-sm">{mp.isAnonymous ? 'Anonymous Member' : 'Luxury Member'}</p>
                             <p className="text-[10px] text-gray-500 uppercase tracking-widest">{mp.mood}</p>
                           </div>
                        </div>
                        <p className="text-gray-200 text-sm italic leading-relaxed mb-6">"{mp.text}"</p>

<div className="flex gap-4">
                           <button className="flex items-center gap-1.5 text-xs text-gray-500 hover:text-red-400 transition-colors">
                             <Heart className="w-4 h-4" /> {mp.reactions?.heart || 0}
                           </button>
                           <button className="flex items-center gap-1.5 text-xs text-gray-500 hover:text-blue-400 transition-colors">
                             <MessageCircle className="w-4 h-4" /> Reply
                           </button>
                        </div>
                      </div>
                    ))}
                  </div>
                )}

                {homeSubTab === 'videos' && (
                  <div className="h-full snap-y snap-mandatory overflow-y-auto no-scrollbar">
                    {posts.filter(p => p.mediaType === 'video').map(p => (
                      <div key={p.id} className="h-screen w-full snap-start bg-black relative flex items-center justify-center">
                         <video 
                           src={p.mediaUrl} 
                           className="w-full h-full object-cover" 
                           autoPlay 
                           loop 
                           muted 
                           style={{ filter: FILTERS[p.filter || 'none'] }}
                         />
                         
                         {/* Interaction Overlay */}
                         <div className="absolute bottom-24 right-4 flex flex-col gap-6 items-center">
                            <div className="flex flex-col items-center">
                               <button className="w-14 h-14 bg-black/40 backdrop-blur-md rounded-full flex items-center justify-center text-white hover:text-red-500 transition-colors border border-white/10">
                                 <Heart className="w-6 h-6" />
                               </button>
                               <span className="text-[10px] font-bold mt-1 shadow-black">{p.likes}</span>
                            </div>
                            <div className="flex flex-col items-center">
                               <button className="w-14 h-14 bg-black/40 backdrop-blur-md rounded-full flex items-center justify-center text-white border border-white/10">
                                 <MessageCircle className="w-6 h-6" />
                               </button>
                               <span className="text-[10px] font-bold mt-1">{p.commentsCount}</span>
                            </div>
                            <div className="flex flex-col items-center">
                               <button className="w-14 h-14 bg-black/40 backdrop-blur-md rounded-full flex items-center justify-center text-white border border-white/10" onClick={() => setIsGiftShopOpen(true)}>
                                 <Gift className="w-6 h-6 text-gold" />
                               </button>
                               <span className="text-[10px] font-bold mt-1">Gifts</span>
                            </div>
                         </div>

                         {/* Info Overlay */}
                         <div className="absolute bottom-24 left-4 right-16">
                            <p className="font-black text-sm mb-2 text-gold">@{p.authorName}</p>
                            <p className="text-xs text-white/90 drop-shadow-md line-clamp-3">{p.text}</p>
                         </div>
                      </div>
                    ))}
                  </div>
                )}
             </div>
          </div>
        )}

        {/* ... More tab content logic ... */}
      </main>

      {/* NAVIGATION BAR */}
      <nav className="fixed bottom-0 left-0 right-0 bg-black-soft/90 backdrop-blur-xl border-t border-gold/20 p-4 pb-8 flex justify-around items-center z-[100]">

<TabButton id="home" icon={Home} label="Home" />
        <TabButton id="explore" icon={Compass} label="Explore" />
        <button 
          onClick={() => setActiveTab('add')}
          className="w-16 h-16 bg-gold text-black rounded-2xl flex items-center justify-center -mt-12 shadow-[0_10px_30px_rgba(212,175,55,0.4)] border-4 border-black hover:scale-110 active:scale-95 transition-all"
        >
          <Plus className="w-8 h-8" />
        </button>
        <TabButton id="inbox" icon={MessageSquare} label="Inbox" />
        <TabButton id="profile" icon={User} label="Profile" />
      </nav>

      {/* TOASTS PORTAL */}
      <div className="fixed top-24 left-1/2 -translate-x-1/2 z-[2000] flex flex-col gap-3 pointer-events-none w-full max-w-xs px-4">
        <AnimatePresence>
          {toasts.map(t => (
            <motion.div 
              key={t.id}
              initial={{ opacity: 0, y: -50, scale: 0.9 }}
              animate={{ opacity: 1, y: 0, scale: 1 }}
              exit={{ opacity: 0, scale: 0.9, y: -20 }}
              className="bg-black/80 backdrop-blur-xl border border-gold/40 rounded-2xl p-4 shadow-2xl flex flex-col gap-1 pointer-events-auto"
            >
              <h4 className="text-gold font-black uppercase tracking-widest text-[10px]">{t.title}</h4>
              <p className="text-white text-xs">{t.text}</p>
            </motion.div>
          ))}
        </AnimatePresence>
      </div>

      {/* VIP MODAL OVERLAY */}
      <AnimatePresence>
        {isVipModalOpen && (
          <motion.div 
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
            className="fixed inset-0 z-[3000] bg-black/90 backdrop-blur-2xl flex items-center justify-center p-6"
          >
            <motion.div 
               initial={{ scale: 0.9, opacity: 0, y: 30 }}
               animate={{ scale: 1, opacity: 1, y: 0 }}
               className="bg-black-soft border border-gold/30 rounded-[3rem] p-8 w-full max-w-md text-center relative overflow-hidden"
            >
              <div className="absolute top-0 left-0 w-full h-1 gold-gradient animate-pulse" />
              <button 
                onClick={() => setIsVipModalOpen(false)}
                className="absolute top-6 right-6 p-2 bg-white/5 rounded-full text-gold hover:bg-white/10"
              >
                <X className="w-5 h-5" />
              </button>
              
              <Crown className="w-20 h-20 text-gold mx-auto mb-6 drop-shadow-[0_0_20px_rgba(212,175,55,0.5)]" />
              <h2 className="text-4xl font-bold mb-2 gold-gradient bg-clip-text text-transparent italic font-serif">Unlock Excellence</h2>
              <p className="text-gray-400 text-sm mb-10">Premium features for the luxury community of melkahayu.nahom</p>
              
              <div className="grid gap-4 mb-10">
                 {['Daily', 'Weekly', 'Monthly'].map(p => (
                   <div 
                     key={p}
                     onClick={() => setSelectedPlan(p.toLowerCase())}
                     className={yn(
                       "p-6 rounded-3xl border transition-all cursor-pointer flex justify-between items-center group",
                       selectedPlan === p.toLowerCase() ? "bg-gold border-gold" : "bg-black/40 border-white/10 hover:border-gold/30"
                     )}
                   >
                     <div className="text-left">
                       <h4 className={yn("font-black uppercase tracking-widest text-xs", selectedPlan === p.toLowerCase() ? "text-black" : "text-gold")}>{p} Elite</h4>
                       <p className={yn("text-[10px] font-medium", selectedPlan === p.toLowerCase() ? "text-black/60" : "text-gray-500")}>Full Access + Offline Mode</p>

</div>
                     <span className={yn("font-bold text-lg", selectedPlan === p.toLowerCase() ? "text-black" : "text-white")}>
                       {p === 'Daily' ? '15' : p === 'Weekly' ? '50' : '150'} ብር
                     </span>
                   </div>
                 ))}
              </div>

              <button className="w-full py-5 bg-gold text-black font-black uppercase text-xs tracking-[0.3em] rounded-3xl hover:bg-gold-light transition-all shadow-[0_20px_40px_rgba(212,175,55,0.2)]">
                Upgrade Now
              </button>
            </motion.div>
          </motion.div>
        )}
      </AnimatePresence>
    </div>
  );
}
