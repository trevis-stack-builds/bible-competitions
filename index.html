import React, { useState, useEffect, useMemo } from 'react';
import { initializeApp } from 'firebase/app';
import { 
  getAuth, 
  signInAnonymously, 
  signInWithCustomToken, 
  onAuthStateChanged 
} from 'firebase/auth';
import { 
  getFirestore, 
  doc, 
  getDoc, 
  setDoc, 
  collection, 
  onSnapshot, 
  updateDoc, 
  addDoc, 
  deleteDoc 
} from 'firebase/firestore';
import { 
  CheckCircle, 
  XCircle, 
  Lock, 
  User, 
  ShieldCheck, 
  Plus, 
  Edit3, 
  Trash2, 
  Send, 
  Play, 
  RotateCcw, 
  Eye, 
  Key, 
  Check, 
  HelpCircle, 
  Sparkles, 
  Award, 
  LogOut, 
  Settings, 
  Layers, 
  Shuffle, 
  BookOpen, 
  ArrowRight,
  List,
  Grid
} from 'lucide-react';

const firebaseConfig = typeof __firebase_config !== 'undefined' 
  ? JSON.parse(__firebase_config) 
  : {
      apiKey: "demo-api-key",
      authDomain: "demo-app.firebaseapp.com",
      projectId: "demo-app",
      storageBucket: "demo-app.appspot.com",
      messagingSenderId: "123456789",
      appId: "1:123456789:web:abcdef"
    };

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
const appId = typeof __app_id !== 'undefined' ? __app_id : 'quiz-app-default';

const INITIAL_USERS = [
  { id: 'u_trevis', username: 'Trevis', role: 'host', pass: '1234567' },
  { id: 'u_john', username: 'John', role: 'user', pass: '1234567' },
  { id: 'u_jeff', username: 'Jeff', role: 'user', pass: '1234567' },
  { id: 'u_dominic', username: 'Dominic', role: 'user', pass: '1234567' },
  { id: 'u_joshua', username: 'Joshua', role: 'user', pass: '1234567' },
  { id: 'u_ivan', username: 'Ivan', role: 'user', pass: '1234567' },
  { id: 'u_anon1', username: 'Anonymous 1', role: 'user', pass: '1234567' },
  { id: 'u_anon2', username: 'Anonymous 2', role: 'user', pass: '1234567' },
  { id: 'u_anon3', username: 'Anonymous 3', role: 'user', pass: '1234567' },
  { id: 'u_anon4', username: 'Anonymous 4', role: 'user', pass: '1234567' },
];

export default function App() {
  const [user, setUser] = useState(null);
  const [currentUserProfile, setCurrentUserProfile] = useState(null);
  const [accounts, setAccounts] = useState([]);
  const [questions, setQuestions] = useState([]);
  const [quizStatus, setQuizStatus] = useState({ isPublished: false, publishedAt: null });
  
  // UI Tabs & Navigation State
  const [activeTab, setActiveTab] = useState('creator'); // 'creator', 'quiz', 'results', 'settings', 'manage_users'
  
  // Login modal / screen state
  const [loginUsername, setLoginUsername] = useState('Trevis');
  const [loginPassword, setLoginPassword] = useState('');
  const [loginError, setLoginError] = useState('');

  // Question Form State (Creation / Editing)
  const [editingQId, setEditingQId] = useState(null);
  const [qType, setQType] = useState('mcq'); // 'mcq', 'fill', 'matching'
  const [qText, setQText] = useState('');
  const [qExplanation, setQExplanation] = useState('');
  
  // Type-specific state
  const [mcqOptions, setMcqOptions] = useState(['', '', '', '']);
  const [mcqCorrect, setMcqCorrect] = useState(0);
  const [fillAnswers, setFillAnswers] = useState(['']);
  const [matchingPairs, setMatchingPairs] = useState([{ left: '', right: '' }, { left: '', right: '' }]);

  // Quiz Execution State
  const [userAnswers, setUserAnswers] = useState({});
  const [quizSubmitted, setQuizSubmitted] = useState(false);
  const [scoreResult, setScoreResult] = useState(null);

  // Settings State
  const [oldPassword, setOldPassword] = useState('');
  const [newPassword, setNewPassword] = useState('');
  const [passMsg, setPassMsg] = useState({ text: '', isError: false });

  // User Management State (Host feature)
  const [newUserUsername, setNewUserUsername] = useState('');
  const [newUserRole, setNewUserRole] = useState('user');

  useEffect(() => {
    const initAuth = async () => {
      try {
        if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
          await signInWithCustomToken(auth, __initial_auth_token);
        } else {
          await signInAnonymously(auth);
        }
      } catch (err) {
        console.error("Auth init error:", err);
      }
    };
    initAuth();
    const unsubscribe = onAuthStateChanged(auth, (u) => {
      setUser(u);
    });
    return () => unsubscribe();
  }, []);

  useEffect(() => {
    if (!user) return;

    // 1. Sync User Accounts (Public artifacts path)
    const accountsRef = collection(db, 'artifacts', appId, 'public', 'data', 'user_accounts');
    const unsubAccounts = onSnapshot(accountsRef, (snapshot) => {
      if (snapshot.empty) {
        // Seed initial 10 accounts if database is empty
        INITIAL_USERS.forEach(u => {
          setDoc(doc(accountsRef, u.id), u);
        });
      } else {
        const accList = [];
        snapshot.forEach(doc => accList.push({ id: doc.id, ...doc.data() }));
        setAccounts(accList);
      }
    }, (err) => console.error("Accounts snapshot error:", err));

    // 2. Sync Quiz Status (Is Published?)
    const statusDocRef = doc(db, 'artifacts', appId, 'public', 'data', 'quiz_meta', 'status');
    const unsubStatus = onSnapshot(statusDocRef, (docSnap) => {
      if (docSnap.exists()) {
        setQuizStatus(docSnap.data());
      } else {
        setDoc(statusDocRef, { isPublished: false, publishedAt: null });
      }
    }, (err) => console.error("Status snapshot error:", err));

    // 3. Sync Questions
    const questionsRef = collection(db, 'artifacts', appId, 'public', 'data', 'questions');
    const unsubQuestions = onSnapshot(questionsRef, (snapshot) => {
      const qList = [];
      snapshot.forEach(d => qList.push({ id: d.id, ...d.data() }));
      setQuestions(qList);
    }, (err) => console.error("Questions snapshot error:", err));

    return () => {
      unsubAccounts();
      unsubStatus();
      unsubQuestions();
    };
  }, [user]);

  const handleLogin = (e) => {
    e.preventDefault();
    setLoginError('');
    const matchedAccount = accounts.find(a => a.username.toLowerCase() === loginUsername.toLowerCase());
    if (!matchedAccount) {
      setLoginError('User account not found!');
      return;
    }
    if (matchedAccount.pass !== loginPassword) {
      setLoginError('Incorrect password! Default password is "1234567"');
      return;
    }
    setCurrentUserProfile(matchedAccount);
    setLoginPassword('');
    setActiveTab(matchedAccount.role === 'host' ? 'creator' : 'creator');
  };

  const handleLogout = () => {
    setCurrentUserProfile(null);
    setUserAnswers({});
    setQuizSubmitted(false);
  };

  const resetQuestionForm = () => {
    setEditingQId(null);
    setQType('mcq');
    setQText('');
    setQExplanation('');
    setMcqOptions(['', '', '', '']);
    setMcqCorrect(0);
    setFillAnswers(['']);
    setMatchingPairs([{ left: '', right: '' }, { left: '', right: '' }]);
  };

  const handleSaveQuestion = async (e) => {
    e.preventDefault();
    if (!qText.trim()) return;

    const payload = {
      authorId: currentUserProfile.id,
      authorName: currentUserProfile.username,
      type: qType,
      text: qText.trim(),
      explanation: qExplanation.trim(),
      updatedAt: Date.now()
    };

    if (qType === 'mcq') {
      const filteredOps = mcqOptions.map(o => o.trim());
      if (filteredOps.some(o => !o)) {
        alert('Please fill out all multiple choice options');
        return;
      }
      payload.options = filteredOps;
      payload.correctOption = parseInt(mcqCorrect);
    } else if (qType === 'fill') {
      const answers = fillAnswers.map(a => a.trim().toLowerCase()).filter(a => a !== '');
      if (answers.length === 0) {
        alert('Please enter at least one accepted fill-in answer');
        return;
      }
      payload.correctAnswers = answers;
    } else if (qType === 'matching') {
      const validPairs = matchingPairs.filter(p => p.left.trim() !== '' && p.right.trim() !== '');
      if (validPairs.length < 2) {
        alert('Please provide at least 2 valid matching pairs');
        return;
      }
      payload.pairs = validPairs.map(p => ({ left: p.left.trim(), right: p.right.trim() }));
    }

    try {
      const questionsRef = collection(db, 'artifacts', appId, 'public', 'data', 'questions');
      if (editingQId) {
        await updateDoc(doc(questionsRef, editingQId), payload);
      } else {
        await addDoc(questionsRef, payload);
      }
      resetQuestionForm();
    } catch (err) {
      console.error("Error saving question:", err);
    }
  };

  const handleEditClick = (q) => {
    setEditingQId(q.id);
    setQType(q.type);
    setQText(q.text);
    setQExplanation(q.explanation || '');
    if (q.type === 'mcq') {
      setMcqOptions(q.options || ['', '', '', '']);
      setMcqCorrect(q.correctOption || 0);
    } else if (q.type === 'fill') {
      setFillAnswers(q.correctAnswers || ['']);
    } else if (q.type === 'matching') {
      setMatchingPairs(q.pairs || [{ left: '', right: '' }, { left: '', right: '' }]);
    }
    // Scroll to form top smoothly
    window.scrollTo({ top: 0, behavior: 'smooth' });
  };

  const handleDeleteQuestion = async (qId) => {
    try {
      await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'questions', qId));
    } catch (err) {
      console.error("Error deleting question:", err);
    }
  };

  const handleTogglePublish = async () => {
    if (currentUserProfile?.role !== 'host') return;
    try {
      const statusDocRef = doc(db, 'artifacts', appId, 'public', 'data', 'quiz_meta', 'status');
      const newStatus = !quizStatus.isPublished;
      await setDoc(statusDocRef, {
        isPublished: newStatus,
        publishedAt: newStatus ? Date.now() : null
      });
    } catch (err) {
      console.error("Error toggling publish state:", err);
    }
  };

  const handleAnswerChange = (qId, val) => {
    setUserAnswers(prev => ({ ...prev, [qId]: val }));
  };

  const calculateScore = () => {
    let score = 0;
    const total = questions.length;
    
    questions.forEach(q => {
      const uAns = userAnswers[q.id];
      if (!uAns) return;

      if (q.type === 'mcq') {
        if (parseInt(uAns) === q.correctOption) score += 1;
      } else if (q.type === 'fill') {
        const cleaned = String(uAns).trim().toLowerCase();
        if (q.correctAnswers.some(ans => ans.toLowerCase() === cleaned)) {
          score += 1;
        }
      } else if (q.type === 'matching') {
        // uAns is expected to be object mapping { [leftText]: selectedRightText }
        let allMatched = true;
        q.pairs.forEach(pair => {
          if (uAns[pair.left] !== pair.right) {
            allMatched = false;
          }
        });
        if (allMatched && Object.keys(uAns).length === q.pairs.length) {
          score += 1;
        }
      }
    });

    setScoreResult({ score, total, percentage: Math.round((score / (total || 1)) * 100) });
    setQuizSubmitted(true);
    setActiveTab('results');
  };

  const handleUpdatePassword = async (e) => {
    e.preventDefault();
    setPassMsg({ text: '', isError: false });

    if (oldPassword !== currentUserProfile.pass) {
      setPassMsg({ text: 'Current password is incorrect!', isError: true });
      return;
    }
    if (newPassword.length < 4) {
      setPassMsg({ text: 'New password must be at least 4 characters long', isError: true });
      return;
    }

    try {
      const userRef = doc(db, 'artifacts', appId, 'public', 'data', 'user_accounts', currentUserProfile.id);
      await updateDoc(userRef, { pass: newPassword });
      setCurrentUserProfile(prev => ({ ...prev, pass: newPassword }));
      setPassMsg({ text: 'Password successfully updated!', isError: false });
      setOldPassword('');
      setNewPassword('');
    } catch (err) {
      setPassMsg({ text: 'Error updating password', isError: true });
    }
  };

  const handleAddUser = async (e) => {
    e.preventDefault();
    if (!newUserUsername.trim()) return;
    const newId = 'u_' + Date.now();
    const newUser = {
      id: newId,
      username: newUserUsername.trim(),
      role: newUserRole,
      pass: '1234567'
    };
    try {
      await setDoc(doc(db, 'artifacts', appId, 'public', 'data', 'user_accounts', newId), newUser);
      setNewUserUsername('');
    } catch (err) {
      console.error("Error adding new user:", err);
    }
  };

  // Users see ONLY their uploaded questions in the creator tab, unless they are the Host (or published)
  const visibleDraftQuestions = useMemo(() => {
    if (!currentUserProfile) return [];
    if (currentUserProfile.role === 'host') {
      return questions; // Host sees all draft questions
    }
    return questions.filter(q => q.authorId === currentUserProfile.id);
  }, [questions, currentUserProfile]);

  if (!currentUserProfile) {
    return (
      <div className="min-h-screen bg-slate-900 text-slate-100 flex items-center justify-center p-4">
        <div className="bg-slate-800 border border-slate-700 rounded-2xl p-6 sm:p-8 w-full max-w-md shadow-2xl space-y-6">
          <div className="text-center space-y-2">
            <div className="inline-flex items-center justify-center w-16 h-16 rounded-2xl bg-indigo-600/20 text-indigo-400 mb-2 border border-indigo-500/30">
              <BookOpen className="w-8 h-8" />
            </div>
            <h1 className="text-2xl font-bold tracking-tight text-white">QuizMaster Portal</h1>
            <p className="text-slate-400 text-sm">Select your account and sign in to continue</p>
          </div>

          <form onSubmit={handleLogin} className="space-y-4">
            <div>
              <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-2">
                Select Account
              </label>
              <select
                value={loginUsername}
                onChange={(e) => setLoginUsername(e.target.value)}
                className="w-full bg-slate-900 border border-slate-700 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-indigo-500 transition-colors"
              >
                {accounts.length > 0 ? (
                  accounts.map(acc => (
                    <option key={acc.id} value={acc.username}>
                      {acc.username} {acc.role === 'host' ? '(Host Account)' : ''}
                    </option>
                  ))
                ) : (
                  INITIAL_USERS.map(acc => (
                    <option key={acc.id} value={acc.username}>
                      {acc.username} {acc.role === 'host' ? '(Host Account)' : ''}
                    </option>
                  ))
                )}
              </select>
            </div>

            <div>
              <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-2">
                Password
              </label>
              <div className="relative">
                <input
                  type="password"
                  value={loginPassword}
                  onChange={(e) => setLoginPassword(e.target.value)}
                  placeholder="Default password: 1234567"
                  className="w-full bg-slate-900 border border-slate-700 rounded-xl px-4 py-3 pl-10 text-white focus:outline-none focus:border-indigo-500 transition-colors"
                  required
                />
                <Lock className="w-5 h-5 text-slate-500 absolute left-3 top-3.5" />
              </div>
            </div>

            {loginError && (
              <div className="bg-red-500/10 border border-red-500/30 text-red-400 text-xs rounded-lg p-3 text-center">
                {loginError}
              </div>
            )}

            <button
              type="submit"
              className="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-semibold py-3 px-4 rounded-xl shadow-lg shadow-indigo-600/30 transition-all active:scale-[0.98]"
            >
              Sign In
            </button>
          </form>

          <div className="border-t border-slate-700/60 pt-4 text-center">
            <p className="text-xs text-slate-500">
              Default password for all accounts: <span className="font-mono text-indigo-400">1234567</span>
            </p>
          </div>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-slate-950 text-slate-100 flex flex-col font-sans">
      {/* Header Bar */}
      <header className="bg-slate-900/80 border-b border-slate-800 backdrop-blur-md sticky top-0 z-50">
        <div className="max-w-6xl mx-auto px-4 py-3 flex items-center justify-between">
          <div className="flex items-center gap-3">
            <div className="w-10 h-10 rounded-xl bg-indigo-600 flex items-center justify-center text-white shadow-md shadow-indigo-600/30">
              <BookOpen className="w-6 h-6" />
            </div>
            <div>
              <h1 className="font-bold text-lg leading-tight text-white">QuizMaster</h1>
              <div className="flex items-center gap-2 text-xs">
                <span className="text-slate-400">LoggedIn as:</span>
                <span className="text-indigo-400 font-semibold">{currentUserProfile.username}</span>
                {currentUserProfile.role === 'host' && (
                  <span className="bg-amber-500/10 text-amber-400 border border-amber-500/30 px-1.5 py-0.5 rounded text-[10px] font-bold">
                    HOST
                  </span>
                )}
              </div>
            </div>
          </div>

          <div className="flex items-center gap-2 sm:gap-4">
            {/* Live Quiz Status Badge */}
            <div className={`hidden sm:flex items-center gap-2 px-3 py-1.5 rounded-full border text-xs font-medium ${
              quizStatus.isPublished 
                ? 'bg-emerald-500/10 border-emerald-500/30 text-emerald-400' 
                : 'bg-amber-500/10 border-amber-500/30 text-amber-400'
            }`}>
              <span className={`w-2 h-2 rounded-full ${quizStatus.isPublished ? 'bg-emerald-500 animate-pulse' : 'bg-amber-500'}`} />
              {quizStatus.isPublished ? 'Quiz Live' : 'Draft Mode'}
            </div>

            <button
              onClick={handleLogout}
              className="flex items-center gap-1.5 text-xs bg-slate-800 hover:bg-slate-700 text-slate-300 px-3 py-2 rounded-lg border border-slate-700 transition-colors"
            >
              <LogOut className="w-4 h-4" />
              <span className="hidden sm:inline">Logout</span>
            </button>
          </div>
        </div>
      </header>

      {/* Navigation Tabs */}
      <nav className="bg-slate-900 border-b border-slate-800">
        <div className="max-w-6xl mx-auto px-4 flex gap-2 overflow-x-auto py-2 scrollbar-none">
          <button
            onClick={() => setActiveTab('creator')}
            className={`flex items-center gap-2 px-4 py-2 rounded-lg text-sm font-medium whitespace-nowrap transition-all ${
              activeTab === 'creator'
                ? 'bg-indigo-600 text-white shadow-md'
                : 'text-slate-400 hover:text-slate-200 hover:bg-slate-800/50'
            }`}
          >
            <Edit3 className="w-4 h-4" />
            Questions Creator
            <span className="ml-1 px-2 py-0.5 rounded-full text-xs bg-slate-900/50">
              {visibleDraftQuestions.length}
            </span>
          </button>

          <button
            onClick={() => setActiveTab('quiz')}
            className={`flex items-center gap-2 px-4 py-2 rounded-lg text-sm font-medium whitespace-nowrap transition-all ${
              activeTab === 'quiz'
                ? 'bg-indigo-600 text-white shadow-md'
                : 'text-slate-400 hover:text-slate-200 hover:bg-slate-800/50'
            }`}
          >
            <Play className="w-4 h-4" />
            Take Quiz
            {quizStatus.isPublished && (
              <span className="w-2 h-2 rounded-full bg-emerald-400 animate-ping" />
            )}
          </button>

          {quizSubmitted && (
            <button
              onClick={() => setActiveTab('results')}
              className={`flex items-center gap-2 px-4 py-2 rounded-lg text-sm font-medium whitespace-nowrap transition-all ${
                activeTab === 'results'
                  ? 'bg-indigo-600 text-white shadow-md'
                  : 'text-slate-400 hover:text-slate-200 hover:bg-slate-800/50'
              }`}
            >
              <Award className="w-4 h-4" />
              Results & Breakdown
            </button>
          )}

          {currentUserProfile.role === 'host' && (
            <button
              onClick={() => setActiveTab('manage_users')}
              className={`flex items-center gap-2 px-4 py-2 rounded-lg text-sm font-medium whitespace-nowrap transition-all ${
                activeTab === 'manage_users'
                  ? 'bg-indigo-600 text-white shadow-md'
                  : 'text-slate-400 hover:text-slate-200 hover:bg-slate-800/50'
              }`}
            >
              <User className="w-4 h-4" />
              Manage Users
            </button>
          )}

          <button
            onClick={() => setActiveTab('settings')}
            className={`flex items-center gap-2 px-4 py-2 rounded-lg text-sm font-medium whitespace-nowrap transition-all ${
              activeTab === 'settings'
                ? 'bg-indigo-600 text-white shadow-md'
                : 'text-slate-400 hover:text-slate-200 hover:bg-slate-800/50'
            }`}
          >
            <Settings className="w-4 h-4" />
            Settings
          </button>
        </div>
      </nav>

      {/* Main Content Area */}
      <main className="flex-1 max-w-6xl w-full mx-auto p-4 sm:p-6">
        {/* ================= TAB 1: QUESTION CREATOR ================= */}
        {activeTab === 'creator' && (
          <div className="space-y-8">
            {/* Host Banner & Control Bar */}
            {currentUserProfile.role === 'host' && (
              <div className="bg-gradient-to-r from-indigo-900/40 via-purple-900/40 to-slate-900 border border-indigo-500/30 rounded-2xl p-5 sm:p-6 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4 shadow-lg">
                <div className="space-y-1">
                  <div className="flex items-center gap-2">
                    <ShieldCheck className="w-5 h-5 text-amber-400" />
                    <h2 className="font-bold text-lg text-white">Host Dashboard Controls</h2>
                  </div>
                  <p className="text-slate-300 text-sm">
                    As Host ({currentUserProfile.username}), you can review all user-submitted questions and publish the quiz for everyone.
                  </p>
                </div>

                <button
                  onClick={handleTogglePublish}
                  className={`w-full sm:w-auto px-6 py-3 rounded-xl font-bold flex items-center justify-center gap-2 shadow-lg transition-all active:scale-95 ${
                    quizStatus.isPublished
                      ? 'bg-amber-600 hover:bg-amber-500 text-white shadow-amber-600/30'
                      : 'bg-emerald-600 hover:bg-emerald-500 text-white shadow-emerald-600/30'
                  }`}
                >
                  <Send className="w-4 h-4" />
                  {quizStatus.isPublished ? 'Unpublish Quiz' : 'Publish All Questions Live'}
                </button>
              </div>
            )}

            {/* Privacy Notice Banner for Regular Users */}
            {currentUserProfile.role !== 'host' && (
              <div className="bg-slate-900 border border-slate-800 rounded-xl p-4 flex items-center gap-3 text-slate-300 text-sm">
                <Lock className="w-5 h-5 text-indigo-400 flex-shrink-0" />
                <span>
                  <strong>Privacy Enabled:</strong> Your drafted questions are completely private and visible only to you until published by the Host.
                </span>
              </div>
            )}

            {/* Form & List Grid */}
            <div className="grid grid-cols-1 lg:grid-cols-12 gap-8">
              {/* Question Creation/Editing Form */}
              <div className="lg:col-span-6 bg-slate-900 border border-slate-800 rounded-2xl p-5 sm:p-6 space-y-6 shadow-xl">
                <div className="flex items-center justify-between border-b border-slate-800 pb-4">
                  <h3 className="font-bold text-lg text-white flex items-center gap-2">
                    <Plus className="w-5 h-5 text-indigo-400" />
                    {editingQId ? 'Edit Question' : 'Add New Question'}
                  </h3>
                  {editingQId && (
                    <button
                      onClick={resetQuestionForm}
                      className="text-xs text-slate-400 hover:text-slate-200 underline"
                    >
                      Cancel Editing
                    </button>
                  )}
                </div>

                <form onSubmit={handleSaveQuestion} className="space-y-5">
                  {/* Question Type Selector */}
                  <div>
                    <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-2">
                      Question Format
                    </label>
                    <div className="grid grid-cols-3 gap-2">
                      {[
                        { id: 'mcq', label: 'Multiple Choice' },
                        { id: 'fill', label: 'Fill in Blanks' },
                        { id: 'matching', label: 'Matching Pairs' }
                      ].map(type => (
                        <button
                          key={type.id}
                          type="button"
                          onClick={() => setQType(type.id)}
                          className={`py-2 px-3 rounded-xl text-xs font-semibold border transition-all ${
                            qType === type.id
                              ? 'bg-indigo-600 border-indigo-500 text-white'
                              : 'bg-slate-950 border-slate-800 text-slate-400 hover:bg-slate-800'
                          }`}
                        >
                          {type.label}
                        </button>
                      ))}
                    </div>
                  </div>

                  {/* Question Prompt */}
                  <div>
                    <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-2">
                      Question Prompt
                    </label>
                    <textarea
                      value={qText}
                      onChange={(e) => setQText(e.target.value)}
                      placeholder="e.g. What is the capital of France?"
                      rows={3}
                      className="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-white text-sm focus:outline-none focus:border-indigo-500 transition-colors"
                      required
                    />
                  </div>

                  {/* Dynamic Fields Based on Question Type */}
                  {/* 1. MCQ OPTIONS */}
                  {qType === 'mcq' && (
                    <div className="space-y-3">
                      <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider">
                        Options (Select the correct radio)
                      </label>
                      {mcqOptions.map((opt, idx) => (
                        <div key={idx} className="flex items-center gap-2">
                          <input
                            type="radio"
                            name="correct_mcq"
                            checked={mcqCorrect === idx}
                            onChange={() => setMcqCorrect(idx)}
                            className="w-4 h-4 text-indigo-600 focus:ring-indigo-500 cursor-pointer"
                          />
                          <input
                            type="text"
                            value={opt}
                            onChange={(e) => {
                              const newOpts = [...mcqOptions];
                              newOpts[idx] = e.target.value;
                              setMcqOptions(newOpts);
                            }}
                            placeholder={`Option ${idx + 1}`}
                            className="flex-1 bg-slate-950 border border-slate-800 rounded-xl px-3 py-2 text-sm text-white focus:outline-none focus:border-indigo-500"
                            required
                          />
                        </div>
                      ))}
                    </div>
                  )}

                  {/* 2. FILL IN THE BLANK ANSWERS */}
                  {qType === 'fill' && (
                    <div className="space-y-3">
                      <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider">
                        Accepted Answer Variations
                      </label>
                      {fillAnswers.map((ans, idx) => (
                        <div key={idx} className="flex items-center gap-2">
                          <input
                            type="text"
                            value={ans}
                            onChange={(e) => {
                              const newAns = [...fillAnswers];
                              newAns[idx] = e.target.value;
                              setFillAnswers(newAns);
                            }}
                            placeholder="e.g. Paris"
                            className="flex-1 bg-slate-950 border border-slate-800 rounded-xl px-3 py-2 text-sm text-white focus:outline-none focus:border-indigo-500"
                            required
                          />
                          {fillAnswers.length > 1 && (
                            <button
                              type="button"
                              onClick={() => setFillAnswers(fillAnswers.filter((_, i) => i !== idx))}
                              className="text-red-400 hover:text-red-300 p-2"
                            >
                              <Trash2 className="w-4 h-4" />
                            </button>
                          )}
                        </div>
                      ))}
                      <button
                        type="button"
                        onClick={() => setFillAnswers([...fillAnswers, ''])}
                        className="text-xs text-indigo-400 font-semibold hover:underline flex items-center gap-1"
                      >
                        <Plus className="w-3 h-3" /> Add Alternative Answer
                      </button>
                    </div>
                  )}

                  {/* 3. MATCHING PAIRS */}
                  {qType === 'matching' && (
                    <div className="space-y-3">
                      <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider">
                        Matching Pairs (Item - Match)
                      </label>
                      {matchingPairs.map((pair, idx) => (
                        <div key={idx} className="grid grid-cols-2 gap-2 items-center">
                          <input
                            type="text"
                            value={pair.left}
                            onChange={(e) => {
                              const newPairs = [...matchingPairs];
                              newPairs[idx].left = e.target.value;
                              setMatchingPairs(newPairs);
                            }}
                            placeholder={`Left Item ${idx + 1}`}
                            className="bg-slate-950 border border-slate-800 rounded-xl px-3 py-2 text-sm text-white focus:outline-none focus:border-indigo-500"
                            required
                          />
                          <div className="flex items-center gap-2">
                            <input
                              type="text"
                              value={pair.right}
                              onChange={(e) => {
                                const newPairs = [...matchingPairs];
                                newPairs[idx].right = e.target.value;
                                setMatchingPairs(newPairs);
                              }}
                              placeholder={`Right Match ${idx + 1}`}
                              className="flex-1 bg-slate-950 border border-slate-800 rounded-xl px-3 py-2 text-sm text-white focus:outline-none focus:border-indigo-500"
                              required
                            />
                            {matchingPairs.length > 2 && (
                              <button
                                type="button"
                                onClick={() => setMatchingPairs(matchingPairs.filter((_, i) => i !== idx))}
                                className="text-red-400 hover:text-red-300 p-1"
                              >
                                <Trash2 className="w-4 h-4" />
                              </button>
                            )}
                          </div>
                        </div>
                      ))}
                      <button
                        type="button"
                        onClick={() => setMatchingPairs([...matchingPairs, { left: '', right: '' }])}
                        className="text-xs text-indigo-400 font-semibold hover:underline flex items-center gap-1"
                      >
                        <Plus className="w-3 h-3" /> Add Pair
                      </button>
                    </div>
                  )}

                  {/* Solution Notes / Explanation */}
                  <div>
                    <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-2">
                      Explanation / Solution Notes (Shown after Quiz)
                    </label>
                    <textarea
                      value={qExplanation}
                      onChange={(e) => setQExplanation(e.target.value)}
                      placeholder="Explain why this answer is correct..."
                      rows={2}
                      className="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-white text-sm focus:outline-none focus:border-indigo-500 transition-colors"
                    />
                  </div>

                  <button
                    type="submit"
                    className="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-semibold py-3 px-4 rounded-xl shadow-lg shadow-indigo-600/30 transition-all active:scale-[0.98]"
                  >
                    {editingQId ? 'Update Question' : 'Save Question to Drafts'}
                  </button>
                </form>
              </div>

              {/* Questions Draft List */}
              <div className="lg:col-span-6 space-y-4">
                <div className="flex items-center justify-between">
                  <h3 className="font-bold text-lg text-white">
                    {currentUserProfile.role === 'host' ? 'All User Drafts' : 'Your Draft Questions'}
                  </h3>
                  <span className="text-xs text-slate-400">
                    {visibleDraftQuestions.length} total questions
                  </span>
                </div>

                {visibleDraftQuestions.length === 0 ? (
                  <div className="bg-slate-900 border border-dashed border-slate-800 rounded-2xl p-8 text-center text-slate-500 space-y-2">
                    <HelpCircle className="w-10 h-10 mx-auto text-slate-600" />
                    <p className="text-sm">No questions created yet.</p>
                    <p className="text-xs text-slate-600">Use the form on the left to start drafting questions.</p>
                  </div>
                ) : (
                  <div className="space-y-3 max-h-[700px] overflow-y-auto pr-1">
                    {visibleDraftQuestions.map((q, idx) => (
                      <div
                        key={q.id}
                        className="bg-slate-900 border border-slate-800 rounded-xl p-4 space-y-3 hover:border-slate-700 transition-colors"
                      >
                        <div className="flex items-start justify-between gap-3">
                          <div className="space-y-1">
                            <div className="flex items-center gap-2">
                              <span className="bg-indigo-500/10 text-indigo-400 border border-indigo-500/20 text-[10px] font-bold px-2 py-0.5 rounded-full uppercase">
                                {q.type}
                              </span>
                              <span className="text-xs text-slate-500">
                                By: <strong className="text-slate-300">{q.authorName}</strong>
                              </span>
                            </div>
                            <p className="font-medium text-white text-sm">
                              {idx + 1}. {q.text}
                            </p>
                          </div>

                          <div className="flex items-center gap-1">
                            <button
                              onClick={() => handleEditClick(q)}
                              className="p-1.5 text-slate-400 hover:text-indigo-400 hover:bg-slate-800 rounded-lg transition-colors"
                              title="Edit"
                            >
                              <Edit3 className="w-4 h-4" />
                            </button>
                            <button
                              onClick={() => handleDeleteQuestion(q.id)}
                              className="p-1.5 text-slate-400 hover:text-red-400 hover:bg-slate-800 rounded-lg transition-colors"
                              title="Delete"
                            >
                              <Trash2 className="w-4 h-4" />
                            </button>
                          </div>
                        </div>

                        {/* Preview details */}
                        <div className="bg-slate-950 rounded-lg p-2.5 text-xs text-slate-400 space-y-1">
                          {q.type === 'mcq' && (
                            <div>Options: {q.options.join(', ')}</div>
                          )}
                          {q.type === 'fill' && (
                            <div>Accepted: {q.correctAnswers.join(', ')}</div>
                          )}
                          {q.type === 'matching' && (
                            <div>
                              Pairs: {q.pairs.map(p => `${p.left} → ${p.right}`).join(' | ')}
                            </div>
                          )}
                          {q.explanation && (
                            <div className="text-slate-500 italic mt-1">
                              Note: {q.explanation}
                            </div>
                          )}
                        </div>
                      </div>
                    ))}
                  </div>
                )}
              </div>
            </div>
          </div>
        )}

        {/* ================= TAB 2: TAKE QUIZ ================= */}
        {activeTab === 'quiz' && (
          <div className="max-w-3xl mx-auto space-y-6">
            {!quizStatus.isPublished ? (
              <div className="bg-slate-900 border border-amber-500/30 rounded-2xl p-8 text-center space-y-4">
                <div className="inline-flex items-center justify-center w-16 h-16 rounded-full bg-amber-500/10 text-amber-400">
                  <Lock className="w-8 h-8" />
                </div>
                <h2 className="text-xl font-bold text-white">Quiz is Currently Offline / Unpublished</h2>
                <p className="text-slate-400 text-sm max-w-md mx-auto">
                  The host account (<strong>Trevis</strong>) needs to click "Publish All Questions Live" from the Questions Creator tab before participants can answer the quiz.
                </p>
              </div>
            ) : questions.length === 0 ? (
              <div className="bg-slate-900 border border-slate-800 rounded-2xl p-8 text-center text-slate-400">
                No questions have been added to this quiz yet!
              </div>
            ) : (
              <div className="space-y-6">
                <div className="bg-slate-900 border border-slate-800 rounded-2xl p-6 space-y-4">
                  <div className="flex items-center justify-between border-b border-slate-800 pb-4">
                    <div>
                      <h2 className="text-xl font-bold text-white">Interactive Assessment</h2>
                      <p className="text-slate-400 text-xs mt-1">Answer all questions below and submit to calculate your score.</p>
                    </div>
                    <span className="bg-indigo-600/20 text-indigo-400 border border-indigo-500/30 text-xs px-3 py-1 rounded-full font-semibold">
                      {questions.length} Questions Total
                    </span>
                  </div>

                  {/* List of Published Questions */}
                  <div className="space-y-8 pt-2">
                    {questions.map((q, idx) => (
                      <div key={q.id} className="bg-slate-950 border border-slate-800 rounded-xl p-5 space-y-4">
                        <div className="flex items-start gap-3">
                          <span className="w-7 h-7 rounded-lg bg-indigo-600/20 text-indigo-400 border border-indigo-500/30 flex items-center justify-center text-sm font-bold flex-shrink-0">
                            {idx + 1}
                          </span>
                          <div>
                            <h3 className="font-semibold text-white text-base">{q.text}</h3>
                            <span className="text-[11px] text-slate-500 uppercase tracking-wider">
                              Format: {q.type}
                            </span>
                          </div>
                        </div>

                        {/* Interactive Question Input Widgets */}
                        <div className="pl-0 sm:pl-10">
                          {/* MCQ Widget */}
                          {q.type === 'mcq' && (
                            <div className="space-y-2">
                              {q.options.map((opt, oIdx) => (
                                <label
                                  key={oIdx}
                                  className={`flex items-center gap-3 p-3 rounded-xl border cursor-pointer transition-all ${
                                    userAnswers[q.id] === oIdx
                                      ? 'bg-indigo-600/20 border-indigo-500 text-white'
                                      : 'bg-slate-900 border-slate-800 text-slate-300 hover:border-slate-700'
                                  }`}
                                >
                                  <input
                                    type="radio"
                                    name={`q_${q.id}`}
                                    checked={userAnswers[q.id] === oIdx}
                                    onChange={() => handleAnswerChange(q.id, oIdx)}
                                    className="w-4 h-4 text-indigo-600 focus:ring-indigo-500"
                                  />
                                  <span className="text-sm">{opt}</span>
                                </label>
                              ))}
                            </div>
                          )}

                          {/* Fill in Blanks Widget */}
                          {q.type === 'fill' && (
                            <div>
                              <input
                                type="text"
                                value={userAnswers[q.id] || ''}
                                onChange={(e) => handleAnswerChange(q.id, e.target.value)}
                                placeholder="Type your answer here..."
                                className="w-full bg-slate-900 border border-slate-800 rounded-xl p-3 text-sm text-white focus:outline-none focus:border-indigo-500 transition-colors"
                              />
                            </div>
                          )}

                          {/* Matching Pair Selection Widget */}
                          {q.type === 'matching' && (
                            <div className="space-y-3">
                              {q.pairs.map((pair, pIdx) => {
                                const currentMap = userAnswers[q.id] || {};
                                return (
                                  <div key={pIdx} className="grid grid-cols-1 sm:grid-cols-2 gap-3 items-center bg-slate-900 border border-slate-800 p-3 rounded-xl">
                                    <div className="text-sm font-medium text-slate-200">
                                      {pair.left}
                                    </div>
                                    <select
                                      value={currentMap[pair.left] || ''}
                                      onChange={(e) => {
                                        const newMap = { ...currentMap, [pair.left]: e.target.value };
                                        handleAnswerChange(q.id, newMap);
                                      }}
                                      className="bg-slate-950 border border-slate-800 rounded-lg p-2 text-xs text-white focus:outline-none focus:border-indigo-500"
                                    >
                                      <option value="">-- Choose Match --</option>
                                      {q.pairs.map((p, rIdx) => (
                                        <option key={rIdx} value={p.right}>
                                          {p.right}
                                        </option>
                                      ))}
                                    </select>
                                  </div>
                                );
                              })}
                            </div>
                          )}
                        </div>
                      </div>
                    ))}
                  </div>

                  <button
                    onClick={calculateScore}
                    className="w-full bg-emerald-600 hover:bg-emerald-500 text-white font-bold py-4 rounded-xl shadow-lg shadow-emerald-600/30 transition-all active:scale-[0.98] flex items-center justify-center gap-2 mt-6"
                  >
                    <CheckCircle className="w-5 h-5" />
                    Submit Quiz & Get Score
                  </button>
                </div>
              </div>
            )}
          </div>
        )}

        {/* ================= TAB 3: RESULTS & BREAKDOWN ================= */}
        {activeTab === 'results' && scoreResult && (
          <div className="max-w-3xl mx-auto space-y-6">
            {/* Score Overview Card */}
            <div className="bg-slate-900 border border-slate-800 rounded-2xl p-6 text-center space-y-4 shadow-xl">
              <div className="inline-flex items-center justify-center w-20 h-20 rounded-full bg-indigo-600/20 text-indigo-400 border border-indigo-500/30">
                <Award className="w-10 h-10" />
              </div>
              <div>
                <h2 className="text-2xl font-bold text-white">Quiz Completed!</h2>
                <p className="text-slate-400 text-sm mt-1">Here is your detailed performance breakdown</p>
              </div>

              <div className="flex justify-center items-center gap-6 py-4 border-y border-slate-800 max-w-sm mx-auto">
                <div>
                  <div className="text-3xl font-extrabold text-indigo-400">
                    {scoreResult.score} / {scoreResult.total}
                  </div>
                  <div className="text-xs text-slate-500 uppercase tracking-wider font-semibold">
                    Correct Answers
                  </div>
                </div>
                <div className="h-10 w-px bg-slate-800" />
                <div>
                  <div className="text-3xl font-extrabold text-emerald-400">
                    {scoreResult.percentage}%
                  </div>
                  <div className="text-xs text-slate-500 uppercase tracking-wider font-semibold">
                    Score
                  </div>
                </div>
              </div>

              <button
                onClick={() => {
                  setUserAnswers({});
                  setQuizSubmitted(false);
                  setActiveTab('quiz');
                }}
                className="inline-flex items-center gap-2 px-5 py-2.5 rounded-xl bg-slate-800 hover:bg-slate-700 text-white text-sm font-semibold border border-slate-700 transition-colors"
              >
                <RotateCcw className="w-4 h-4" />
                Retake Quiz
              </button>
            </div>

            {/* Detailed Question Review */}
            <div className="space-y-4">
              <h3 className="font-bold text-lg text-white">Solutions & Breakdown</h3>

              {questions.map((q, idx) => {
                const uAns = userAnswers[q.id];
                let isCorrect = false;

                if (q.type === 'mcq') {
                  isCorrect = parseInt(uAns) === q.correctOption;
                } else if (q.type === 'fill') {
                  const cleaned = String(uAns || '').trim().toLowerCase();
                  isCorrect = q.correctAnswers.some(ans => ans.toLowerCase() === cleaned);
                } else if (q.type === 'matching') {
                  let allMatched = true;
                  q.pairs.forEach(pair => {
                    if (!uAns || uAns[pair.left] !== pair.right) allMatched = false;
                  });
                  isCorrect = allMatched && Object.keys(uAns || {}).length === q.pairs.length;
                }

                return (
                  <div
                    key={q.id}
                    className={`bg-slate-900 border rounded-2xl p-5 space-y-4 ${
                      isCorrect ? 'border-emerald-500/30' : 'border-red-500/30'
                    }`}
                  >
                    <div className="flex items-start justify-between gap-3">
                      <div className="flex items-start gap-3">
                        {isCorrect ? (
                          <CheckCircle className="w-6 h-6 text-emerald-400 flex-shrink-0 mt-0.5" />
                        ) : (
                          <XCircle className="w-6 h-6 text-red-400 flex-shrink-0 mt-0.5" />
                        )}
                        <div>
                          <h4 className="font-semibold text-white text-base">
                            {idx + 1}. {q.text}
                          </h4>
                          <span className="text-[11px] text-slate-500 uppercase tracking-wider">
                            Type: {q.type}
                          </span>
                        </div>
                      </div>

                      <span className={`px-2.5 py-1 rounded-full text-xs font-bold ${
                        isCorrect
                          ? 'bg-emerald-500/10 text-emerald-400 border border-emerald-500/30'
                          : 'bg-red-500/10 text-red-400 border border-red-500/30'
                      }`}>
                        {isCorrect ? 'Correct' : 'Incorrect'}
                      </span>
                    </div>

                    {/* Breakdown details */}
                    <div className="bg-slate-950 rounded-xl p-4 space-y-2 text-xs">
                      {q.type === 'mcq' && (
                        <>
                          <div className="text-slate-300">
                            <strong>Your Answer:</strong> {uAns !== undefined ? q.options[uAns] : 'None'}
                          </div>
                          <div className="text-emerald-400">
                            <strong>Correct Solution:</strong> {q.options[q.correctOption]}
                          </div>
                        </>
                      )}

                      {q.type === 'fill' && (
                        <>
                          <div className="text-slate-300">
                            <strong>Your Answer:</strong> {uAns || 'None'}
                          </div>
                          <div className="text-emerald-400">
                            <strong>Accepted Solutions:</strong> {q.correctAnswers.join(', ')}
                          </div>
                        </>
                      )}

                      {q.type === 'matching' && (
                        <div className="space-y-1">
                          <strong className="text-slate-300">Your Pairings vs Solutions:</strong>
                          <div className="grid grid-cols-1 gap-1 pt-1">
                            {q.pairs.map((pair, pIdx) => {
                              const chosen = uAns ? uAns[pair.left] : 'None';
                              const matchOk = chosen === pair.right;
                              return (
                                <div key={pIdx} className="flex items-center justify-between border-b border-slate-800/50 py-1">
                                  <span className="text-slate-400">{pair.left}</span>
                                  <span className={matchOk ? 'text-emerald-400' : 'text-red-400'}>
                                    Your choice: {chosen} | Correct: {pair.right}
                                  </span>
                                </div>
                              );
                            })}
                          </div>
                        </div>
                      )}

                      {q.explanation && (
                        <div className="mt-2 pt-2 border-t border-slate-800/80 text-slate-400 italic">
                          💡 <strong>Explanation:</strong> {q.explanation}
                        </div>
                      )}
                    </div>
                  </div>
                );
              })}
            </div>
          </div>
        )}

        {/* ================= TAB 4: MANAGE USERS (HOST ONLY) ================= */}
        {activeTab === 'manage_users' && currentUserProfile.role === 'host' && (
          <div className="max-w-3xl mx-auto space-y-6">
            <div className="bg-slate-900 border border-slate-800 rounded-2xl p-6 space-y-6 shadow-xl">
              <div className="border-b border-slate-800 pb-4">
                <h2 className="text-xl font-bold text-white flex items-center gap-2">
                  <User className="w-5 h-5 text-indigo-400" />
                  User Accounts Directory ({accounts.length})
                </h2>
                <p className="text-slate-400 text-xs mt-1">
                  Manage active participants and host user privileges.
                </p>
              </div>

              {/* Add New User Slot Form */}
              <form onSubmit={handleAddUser} className="bg-slate-950 border border-slate-800 rounded-xl p-4 flex flex-col sm:flex-row gap-3 items-end">
                <div className="flex-1 w-full">
                  <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-1">
                    Username
                  </label>
                  <input
                    type="text"
                    value={newUserUsername}
                    onChange={(e) => setNewUserUsername(e.target.value)}
                    placeholder="New User Name"
                    className="w-full bg-slate-900 border border-slate-800 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-indigo-500"
                    required
                  />
                </div>

                <div className="w-full sm:w-36">
                  <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-1">
                    Role
                  </label>
                  <select
                    value={newUserRole}
                    onChange={(e) => setNewUserRole(e.target.value)}
                    className="w-full bg-slate-900 border border-slate-800 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-indigo-500"
                  >
                    <option value="user">Participant</option>
                    <option value="host">Host</option>
                  </select>
                </div>

                <button
                  type="submit"
                  className="w-full sm:w-auto bg-indigo-600 hover:bg-indigo-500 text-white font-semibold px-4 py-2 rounded-lg text-sm transition-colors flex items-center justify-center gap-1"
                >
                  <Plus className="w-4 h-4" /> Add User
                </button>
              </form>

              {/* Account List Table */}
              <div className="divide-y divide-slate-800 border border-slate-800 rounded-xl overflow-hidden">
                {accounts.map(acc => (
                  <div key={acc.id} className="p-4 bg-slate-950 flex items-center justify-between">
                    <div className="flex items-center gap-3">
                      <div className="w-9 h-9 rounded-full bg-slate-800 flex items-center justify-center text-slate-300 font-bold text-sm">
                        {acc.username.charAt(0).toUpperCase()}
                      </div>
                      <div>
                        <div className="font-semibold text-white text-sm flex items-center gap-2">
                          {acc.username}
                          {acc.role === 'host' && (
                            <span className="bg-amber-500/10 text-amber-400 border border-amber-500/30 text-[10px] font-bold px-1.5 py-0.5 rounded">
                              HOST
                            </span>
                          )}
                        </div>
                        <div className="text-xs text-slate-500">ID: {acc.id}</div>
                      </div>
                    </div>

                    <div className="text-right text-xs">
                      <span className="text-slate-400 font-mono">Password Masked</span>
                    </div>
                  </div>
                ))}
              </div>
            </div>
          </div>
        )}

        {/* ================= TAB 5: SETTINGS ================= */}
        {activeTab === 'settings' && (
          <div className="max-w-md mx-auto space-y-6">
            <div className="bg-slate-900 border border-slate-800 rounded-2xl p-6 space-y-6 shadow-xl">
              <div className="border-b border-slate-800 pb-4">
                <h2 className="text-xl font-bold text-white flex items-center gap-2">
                  <Key className="w-5 h-5 text-indigo-400" />
                  Account Security Settings
                </h2>
                <p className="text-slate-400 text-xs mt-1">
                  Update your account password for <strong>{currentUserProfile.username}</strong>
                </p>
              </div>

              <form onSubmit={handleUpdatePassword} className="space-y-4">
                <div>
                  <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-2">
                    Current Password
                  </label>
                  <input
                    type="password"
                    value={oldPassword}
                    onChange={(e) => setOldPassword(e.target.value)}
                    placeholder="Enter current password"
                    className="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-sm text-white focus:outline-none focus:border-indigo-500 transition-colors"
                    required
                  />
                </div>

                <div>
                  <label className="block text-xs font-semibold text-slate-400 uppercase tracking-wider mb-2">
                    New Password
                  </label>
                  <input
                    type="password"
                    value={newPassword}
                    onChange={(e) => setNewPassword(e.target.value)}
                    placeholder="Enter new password"
                    className="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-sm text-white focus:outline-none focus:border-indigo-500 transition-colors"
                    required
                  />
                </div>

                {passMsg.text && (
                  <div className={`p-3 rounded-lg text-xs text-center border ${
                    passMsg.isError
                      ? 'bg-red-500/10 border-red-500/30 text-red-400'
                      : 'bg-emerald-500/10 border-emerald-500/30 text-emerald-400'
                  }`}>
                    {passMsg.text}
                  </div>
                )}

                <button
                  type="submit"
                  className="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-semibold py-3 px-4 rounded-xl shadow-lg shadow-indigo-600/30 transition-all active:scale-[0.98]"
                >
                  Update Password
                </button>
              </form>
            </div>
          </div>
        )}
      </main>
    </div>
  );
}
