<!DOCTYPE html>
<html lang="bn" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>ভিডিওফ্লো প্রো - প্রফেশনাল ভিডিও ও শর্টস প্ল্যাটফর্ম</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        darkbg: '#0f0f0f',
                        cardbg: '#1a1a1a',
                        hoverbg: '#272727',
                        accentred: '#ff0033'
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts: Hind Siliguri -->
    <link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Hind Siliguri', sans-serif;
            -webkit-tap-highlight-color: transparent;
            overscroll-behavior-y: none;
            touch-action: manipulation;
        }
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0f0f0f;
        }
        ::-webkit-scrollbar-thumb {
            background: #3f3f3f;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #555;
        }
        .sidebar-drawer {
            transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .short-card-aspect {
            aspect-ratio: 9 / 16;
        }
        .long-card-aspect {
            aspect-ratio: 16 / 9;
        }
        .auto-hide-nav {
            transition: transform 0.35s cubic-bezier(0.4, 0, 0.2, 1), opacity 0.35s ease;
            padding-bottom: max(10px, env(safe-area-inset-bottom));
        }
        .nav-hidden {
            transform: translateY(120%);
            opacity: 0;
            pointer-events: none;
        }
    </style>
</head>
<body class="bg-darkbg text-zinc-100 min-h-screen flex flex-col selection:bg-red-600 selection:text-white pb-24 md:pb-0 overflow-x-hidden">

    <header class="sticky top-0 z-50 bg-darkbg/95 backdrop-blur border-b border-zinc-800/80 px-4 py-2.5 flex items-center justify-between">
        <div class="flex items-center space-x-3">
            <button onclick="toggleSidebar()" class="p-2.5 hover:bg-hoverbg rounded-full text-zinc-200 transition focus:outline-none" title="মেনু টগল করুন">
                <i class="fa-solid fa-bars text-lg"></i>
            </button>
            <div class="flex items-center space-x-2 cursor-pointer select-none" onclick="switchTab('home')">
                <div class="bg-red-600 text-white w-9 h-9 rounded-xl flex items-center justify-center shadow-lg shadow-red-600/30 shrink-0">
                    <i class="fa-solid fa-play text-sm"></i>
                </div>
                <span class="text-xl font-bold tracking-tight bg-gradient-to-r from-white via-zinc-200 to-zinc-400 bg-clip-text text-transparent truncate max-w-[120px] sm:max-w-none" id="appTitleText">ভিডিওফ্লো প্রো</span>
            </div>
        </div>

        <div class="flex items-center space-x-1 sm:space-x-2">
            <button onclick="toggleSearchModal()" class="w-10 h-10 rounded-full hover:bg-hoverbg flex items-center justify-center text-zinc-200 transition shrink-0" title="সার্চ করুন">
                <i class="fa-solid fa-magnifying-glass text-lg"></i>
            </button>
            <button onclick="openNotificationsModal()" class="relative w-10 h-10 rounded-full hover:bg-hoverbg flex items-center justify-center text-zinc-200 transition shrink-0" title="নোটিফিকেশন">
                <i class="fa-regular fa-bell text-lg"></i>
                <span class="absolute top-2 right-2 w-2 h-2 bg-red-600 rounded-full"></span>
            </button>
        </div>
    </header>

    <div class="flex flex-1 overflow-hidden relative" id="appBodyContainer">
        <!-- Sidebar Backdrop -->
        <div id="sidebarBackdrop" class="fixed inset-0 bg-black/60 z-40 lg:hidden hidden transition-opacity" onclick="toggleSidebar()"></div>
        
        <!-- Sidebar with YouTube Features -->
        <aside id="sidebar" class="sidebar-drawer fixed lg:static top-0 left-0 h-full lg:h-auto w-64 bg-darkbg border-r border-zinc-800/80 flex flex-col p-3 space-y-4 overflow-y-auto z-50 transform -translate-x-full lg:translate-x-0 shrink-0">
            <div class="flex items-center justify-between px-2 pt-2 lg:hidden">
                <span class="font-bold text-base text-zinc-300" id="sidebarMenuTitle">মেনু বার</span>
                <button onclick="toggleSidebar()" class="p-2 text-zinc-400 hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            
            <div class="space-y-1">
                <button onclick="switchTab('home'); toggleSidebarMobileOnly();" class="w-full flex items-center space-x-4 px-4 py-2.5 rounded-xl hover:bg-hoverbg text-zinc-300 hover:text-white transition text-left cursor-pointer">
                    <i class="fa-solid fa-house w-6 text-center text-lg text-red-500"></i>
                    <span class="font-medium text-sm" id="sidebarHome">হোম</span>
                </button>
                <button onclick="switchTab('shorts'); toggleSidebarMobileOnly();" class="w-full flex items-center space-x-4 px-4 py-2.5 rounded-xl hover:bg-hoverbg text-zinc-300 hover:text-white transition text-left cursor-pointer">
                    <i class="fa-solid fa-bolt w-6 text-center text-lg text-yellow-500"></i>
                    <span class="font-medium text-sm" id="sidebarShorts">শর্টস</span>
                </button>
                <button onclick="switchTab('subscriptions'); toggleSidebarMobileOnly();" class="w-full flex items-center space-x-4 px-4 py-2.5 rounded-xl hover:bg-hoverbg text-zinc-300 hover:text-white transition text-left cursor-pointer">
                    <i class="fa-solid fa-users w-6 text-center text-lg text-blue-400"></i>
                    <span class="font-medium text-sm" id="sidebarSubs">সাবস্ক্রিপশন</span>
                </button>
            </div>

            <hr class="border-zinc-800">

            <div class="space-y-1">
                <h3 class="px-4 text-xs font-semibold text-zinc-400 uppercase tracking-wider" id="sidebarLibTitle">আপনার লাইব্রেরি</h3>
                <button onclick="switchTab('history'); toggleSidebarMobileOnly();" class="w-full flex items-center space-x-4 px-4 py-2.5 rounded-xl hover:bg-hoverbg text-zinc-300 hover:text-white transition text-left cursor-pointer">
                    <i class="fa-solid fa-clock-rotate-left w-6 text-center text-lg"></i>
                    <span id="sidebarHistory" class="text-sm">ইতিহাস</span>
                </button>
                <button onclick="openStudio(); toggleSidebarMobileOnly();" class="w-full flex items-center space-x-4 px-4 py-2.5 rounded-xl hover:bg-hoverbg text-zinc-300 hover:text-white transition text-left cursor-pointer">
                    <i class="fa-solid fa-gauge-high w-6 text-center text-lg"></i>
                    <span id="sidebarStudio" class="text-sm">স্টুডিও ও আপলোড</span>
                </button>
                <button onclick="switchTab('liked'); toggleSidebarMobileOnly();" class="w-full flex items-center space-x-4 px-4 py-2.5 rounded-xl hover:bg-hoverbg text-zinc-300 hover:text-white transition text-left cursor-pointer">
                    <i class="fa-solid fa-thumbs-up w-6 text-center text-lg"></i>
                    <span id="sidebarLiked" class="text-sm">পছন্দ করা ভিডিও</span>
                </button>
                <button onclick="switchTab('playlists'); toggleSidebarMobileOnly();" class="w-full flex items-center space-x-4 px-4 py-2.5 rounded-xl hover:bg-hoverbg text-zinc-300 hover:text-white transition text-left cursor-pointer">
                    <i class="fa-solid fa-list w-6 text-center text-emerald-400 text-lg"></i>
                    <span id="sidebarPlaylists" class="text-sm">প্লেলিস্টসমূহ</span>
                </button>
            </div>

            <hr class="border-zinc-800">

            <div class="space-y-1">
                <h3 class="px-4 text-xs font-semibold text-zinc-400 uppercase tracking-wider" id="sidebarExploreTitle">এক্সপ্লোর ও ফিচার</h3>
                <button onclick="switchTab('home', 'মিউজিক'); toggleSidebarMobileOnly();" class="w-full flex items-center space-x-4 px-4 py-2.5 rounded-xl hover:bg-hoverbg text-zinc-300 hover:text-white transition text-left cursor-pointer">
                    <i class="fa-solid fa-music w-6 text-center text-pink-500 text-lg"></i>
                    <span class="text-sm" id="expMusic">মিউজিক ও গান</span>
                </button>
                <button onclick="switchTab('home', 'টেকনোলজি'); toggleSidebarMobileOnly();" class="w-full flex items-center space-x-4 px-4 py-2.5 rounded-xl hover:bg-hoverbg text-zinc-300 hover:text-white transition text-left cursor-pointer">
                    <i class="fa-solid fa-gamepad w-6 text-center text-purple-400 text-lg"></i>
                    <span class="text-sm" id="expTech">গেমিং ও টেক</span>
                </button>
                <button onclick="switchTab('home', 'সিনেমা ও নাটক'); toggleSidebarMobileOnly();" class="w-full flex items-center space-x-4 px-4 py-2.5 rounded-xl hover:bg-hoverbg text-zinc-300 hover:text-white transition text-left cursor-pointer">
                    <i class="fa-solid fa-film w-6 text-center text-red-500 text-lg"></i>
                    <span class="text-sm" id="expCinema">মুভি ও সিনেমা</span>
                </button>
                <button onclick="switchTab('home', 'ভ্রমণ'); toggleSidebarMobileOnly();" class="w-full flex items-center space-x-4 px-4 py-2.5 rounded-xl hover:bg-hoverbg text-zinc-300 hover:text-white transition text-left cursor-pointer">
                    <i class="fa-solid fa-earth-americas w-6 text-center text-emerald-400 text-lg"></i>
                    <span class="text-sm" id="expTravel">ভ্রমণ ও প্রকৃতি</span>
                </button>
            </div>

            <hr class="border-zinc-800">
            <div class="px-4 text-xs text-zinc-500 space-y-2">
                <p>&copy; ২০২৬ ভিডিওফ্লো প্রো</p>
                <p id="sidebarFooterDesc">সম্পূর্ণ ফিচার ইন্টিগ্রেটেড সংস্করণ।</p>
            </div>
        </aside>

        <!-- Main Content Area -->
        <main id="mainContent" class="flex-1 overflow-y-auto p-4 sm:p-8 bg-darkbg mb-16 md:mb-0">
            <!-- Dynamic content injected here -->
        </main>
    </div>

    <nav id="bottomNavBar" class="auto-hide-nav fixed bottom-0 left-0 right-0 bg-darkbg/95 backdrop-blur border-t border-zinc-800/80 px-2 py-2 grid grid-cols-5 items-center z-50 md:hidden select-none shadow-2xl">
        <button onclick="switchTab('home')" class="flex flex-col items-center space-y-1 text-zinc-400 hover:text-white transition group py-1 cursor-pointer" id="nav-home">
            <i class="fa-solid fa-house text-lg text-red-500"></i>
            <span class="text-[10px] font-medium" id="bottomNavHome">হোম</span>
        </button>
        <button onclick="switchTab('shorts')" class="flex flex-col items-center space-y-1 text-zinc-400 hover:text-white transition group py-1 cursor-pointer" id="nav-shorts">
            <i class="fa-solid fa-bolt text-lg"></i>
            <span class="text-[10px] font-medium" id="bottomNavShorts">শর্টস</span>
        </button>
        <div class="flex items-center justify-center pb-0.5">
            <button onclick="openUploadModal()" class="w-12 h-12 bg-gradient-to-r from-red-600 to-rose-600 rounded-full flex items-center justify-center text-white shadow-lg shadow-red-600/40 hover:scale-105 transition transform active:scale-95 cursor-pointer" title="ভিডিও আপলোড">
                <i class="fa-solid fa-plus text-xl"></i>
            </button>
        </div>
        <button onclick="switchTab('subscriptions')" class="flex flex-col items-center space-y-1 text-zinc-400 hover:text-white transition group py-1 cursor-pointer" id="nav-subscriptions">
            <i class="fa-solid fa-users text-lg"></i>
            <span class="text-[10px] font-medium" id="bottomNavSubs">সাবস্ক্রিপশন</span>
        </button>
        <button onclick="switchTab('profile')" class="flex flex-col items-center space-y-1 text-zinc-400 hover:text-white transition group py-1 cursor-pointer" id="nav-profile">
            <i class="fa-solid fa-circle-user text-lg"></i>
            <span class="text-[10px] font-medium" id="navProfileText">প্রোফাইল</span>
        </button>
    </nav>

    <!-- Language Settings Modal -->
    <div id="languageModal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-cardbg border border-zinc-700 w-full max-w-md rounded-2xl shadow-2xl overflow-hidden flex flex-col max-h-[85vh]">
            <div class="px-6 py-4 border-b border-zinc-700 flex items-center justify-between">
                <h3 class="font-bold text-lg flex items-center space-x-2 text-white">
                    <i class="fa-solid fa-globe text-emerald-400"></i>
                    <span id="langModalTitle">ভাষা নির্বাচন করুন (Select Language)</span>
                </h3>
                <button onclick="closeLanguageModal()" class="text-zinc-400 hover:text-white p-2 cursor-pointer">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            <div class="p-4 overflow-y-auto space-y-2.5 flex-1" id="languageListContainer">
                <!-- Dynamic Language Options -->
            </div>
        </div>
    </div>

    <!-- Bottom Edge Gesture Trigger Area for bringing back the navbar -->
    <div id="bottomGestureArea" class="fixed bottom-0 left-0 right-0 h-6 z-40 md:hidden cursor-pointer"></div>

    <div id="searchModal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-start justify-center pt-16 px-4">
        <div class="bg-cardbg border border-zinc-700 w-full max-w-xl rounded-2xl shadow-2xl p-4 space-y-4">
            <div class="flex items-center space-x-3">
                <div class="flex flex-1 items-center bg-zinc-900 border border-zinc-700 rounded-xl px-4 py-2.5 focus-within:border-red-500">
                    <i class="fa-solid fa-magnifying-glass text-zinc-400 mr-3"></i>
                    <input type="text" id="searchInput" placeholder="ভিডিও বা চ্যানেল অনুসন্ধান করুন..." class="w-full bg-transparent focus:outline-none text-zinc-200 text-sm" onkeydown="if(event.key === 'Enter') { handleSearchModalInput(); }">
                </div>
                <button onclick="toggleSearchModal()" class="text-zinc-400 hover:text-white p-2 cursor-pointer">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            <div class="flex items-center space-x-2 overflow-x-auto pb-1 text-xs">
                <button onclick="quickSearchTag('মিউজিক')" class="bg-zinc-800 hover:bg-zinc-700 px-3 py-1 rounded-full text-zinc-300 whitespace-nowrap cursor-pointer">🎵 মিউজিক</button>
                <button onclick="quickSearchTag('কোডিং')" class="bg-zinc-800 hover:bg-zinc-700 px-3 py-1 rounded-full text-zinc-300 whitespace-nowrap cursor-pointer">💻 কোডিং</button>
                <button onclick="quickSearchTag('সিনেমা')" class="bg-zinc-800 hover:bg-zinc-700 px-3 py-1 rounded-full text-zinc-300 whitespace-nowrap cursor-pointer">🎬 সিনেমা</button>
                <button onclick="quickSearchTag('ভ্রমণ')" class="bg-zinc-800 hover:bg-zinc-700 px-3 py-1 rounded-full text-zinc-300 whitespace-nowrap cursor-pointer">🌍 ভ্রমণ</button>
            </div>
        </div>
    </div>

    <div id="notificationsModal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-cardbg border border-zinc-700 w-full max-w-md rounded-2xl shadow-2xl overflow-hidden flex flex-col max-h-[80vh]">
            <div class="px-6 py-4 border-b border-zinc-700 flex items-center justify-between">
                <h3 class="font-bold text-lg flex items-center space-x-2">
                    <i class="fa-solid fa-bell text-red-500"></i>
                    <span id="notifModalTitle">নোটিফিকেশনসমূহ</span>
                </h3>
                <button onclick="closeNotificationsModal()" class="text-zinc-400 hover:text-white p-2 cursor-pointer">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            <div class="p-4 overflow-y-auto space-y-3 flex-1 divide-y divide-zinc-800" id="notificationsListContainer">
                <div class="flex items-start space-x-3 pt-2">
                    <div class="w-10 h-10 rounded-full bg-red-600/20 text-red-500 flex items-center justify-center shrink-0">
                        <i class="fa-solid fa-video"></i>
                    </div>
                    <div>
                        <h4 class="text-sm font-semibold" id="notifItemTitle">কোডিং গুরু বাংলাদেশ নতুন ভিডিও আপলোড করেছে</h4>
                        <p class="text-xs text-zinc-400 mt-0.5" id="notifItemDesc">সম্পূর্ণ ৫ ঘণ্টার জাভাস্ক্রিপ্ট ও রিয়্যাক্ট মাস্টারক্লাস মেগা প্রজেক্ট</p>
                        <span class="text-[10px] text-zinc-500" id="notifItemTime">২ ঘণ্টা আগে</span>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Enhanced Video Upload Modal -->
    <div id="uploadModal" class="fixed inset-0 bg-black/85 backdrop-blur-md z-50 hidden flex items-center justify-center p-4">
        <div class="bg-cardbg border border-zinc-700 w-full max-w-2xl rounded-2xl shadow-2xl overflow-hidden flex flex-col max-h-[95vh]">
            <div class="px-6 py-4 border-b border-zinc-700 flex items-center justify-between bg-zinc-900/50">
                <h2 class="text-xl font-bold flex items-center space-x-2">
                    <i class="fa-solid fa-cloud-arrow-up text-red-500"></i>
                    <span id="uploadModalMainTitle">নতুন ভিডিও আপলোড করুন</span>
                </h2>
                <button onclick="closeUploadModal()" class="text-zinc-400 hover:text-white p-2 rounded-full hover:bg-zinc-700 transition cursor-pointer">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            
            <div class="p-6 overflow-y-auto space-y-5 flex-1">
                <div class="space-y-2">
                    <label class="block text-sm font-medium text-zinc-300" id="uploadTypeLabel">ভিডিওর ধরন নির্বাচন করুন *</label>
                    <div class="grid grid-cols-2 gap-4">
                        <button type="button" id="typeLongBtn" onclick="setVideoType('long')" class="p-4 rounded-xl border-2 border-red-500 bg-red-500/10 text-left transition flex items-center space-x-3 cursor-pointer">
                            <div class="w-10 h-10 rounded-lg bg-red-600 text-white flex items-center justify-center text-lg"><i class="fa-solid fa-film"></i></div>
                            <div>
                                <h4 class="font-bold text-sm" id="longVidCardTitle">লং ভিডিও (১৬:৯)</h4>
                                <p class="text-[11px] text-zinc-400" id="longVidCardDesc">দীর্ঘ সিনেমা বা ভিডিও</p>
                            </div>
                        </button>
                        <button type="button" id="typeShortBtn" onclick="setVideoType('short')" class="p-4 rounded-xl border-2 border-zinc-700 bg-zinc-900 text-left transition flex items-center space-x-3 cursor-pointer">
                            <div class="w-10 h-10 rounded-lg bg-yellow-500 text-black flex items-center justify-center text-lg"><i class="fa-solid fa-bolt"></i></div>
                            <div>
                                <h4 class="font-bold text-sm" id="shortVidCardTitle">শর্টস ভিডিও (৯:১৬)</h4>
                                <p class="text-[11px] text-zinc-400" id="shortVidCardDesc">ভার্টিকাল ক্লিপ</p>
                            </div>
                        </button>
                    </div>
                </div>

                <div id="dropZone" class="border-2 border-dashed border-zinc-600 rounded-2xl p-8 text-center hover:border-red-500 transition cursor-pointer bg-zinc-900/40" onclick="document.getElementById('videoFileInput').click()">
                    <div class="w-16 h-16 bg-zinc-800 rounded-full flex items-center justify-center mx-auto mb-4 text-red-500 text-2xl shadow-inner">
                        <i class="fa-solid fa-video"></i>
                    </div>
                    <p class="font-semibold text-lg mb-1" id="dropZoneText">ভিডিও ফাইল এখানে ড্রপ করুন</p>
                    <p class="text-xs text-zinc-400 mb-4" id="dropZoneSubText">MP4, MKV বা WebM ফাইল সিলেক্ট করুন</p>
                    <button type="button" id="dropZoneBtn" class="bg-red-600 hover:bg-red-700 text-white px-6 py-2.5 rounded-full font-medium transition shadow-lg shadow-red-600/30 text-sm pointer-events-none">
                        ফাইল সিলেক্ট করুন (ব্রাউজ)
                    </button>
                    <input type="file" id="videoFileInput" accept="video/*" class="hidden" onchange="handleFileSelect(event)">
                </div>

                <div id="uploadProgressContainer" class="hidden space-y-2 bg-zinc-900 p-4 rounded-xl border border-zinc-800">
                    <div class="flex justify-between text-xs font-semibold text-zinc-300">
                        <span id="progressStatusText">ব্রাউজার এআই মডারেশন স্ক্যান চলছে...</span>
                        <span id="progressPercent">০%</span>
                    </div>
                    <div class="w-full bg-zinc-800 h-2.5 rounded-full overflow-hidden">
                        <div id="progressBarFill" class="bg-red-600 h-full w-0 transition-all duration-200"></div>
                    </div>
                </div>

                <div id="uploadFormFields" class="space-y-4 hidden">
                    <div class="flex items-center space-x-4 bg-zinc-900 p-3.5 rounded-xl border border-zinc-800">
                        <i id="selectedFileIcon" class="fa-solid fa-file-video text-red-500 text-xl"></i>
                        <div id="selectedFileName" class="text-sm font-medium text-zinc-200 truncate flex-1">video.mp4</div>
                        <span id="selectedFileBadge" class="text-xs bg-emerald-500/20 text-emerald-400 px-2.5 py-1 rounded-full font-medium">অনুমোদিত</span>
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-zinc-300 mb-1" id="labelVidTitle">ভিডিও শিরোনাম *</label>
                        <input type="text" id="uploadTitle" placeholder="ভিডিওর শিরোনাম দিন..." class="w-full bg-zinc-900 border border-zinc-700 rounded-xl px-4 py-2.5 focus:outline-none focus:border-red-500 text-zinc-200 text-sm">
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-zinc-300 mb-1" id="labelChannelName">চ্যানেলের নাম</label>
                            <input type="text" id="uploadChannel" value="প্রফেশনাল ক্রিয়েটর" class="w-full bg-zinc-900 border border-zinc-700 rounded-xl px-4 py-2.5 focus:outline-none focus:border-red-500 text-zinc-200 text-sm">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-zinc-300 mb-1" id="labelCategory">কনটেন্ট ক্যাটাগরি *</label>
                            <select id="uploadCategory" class="w-full bg-zinc-900 border border-zinc-700 rounded-xl px-4 py-2.5 focus:outline-none focus:border-red-500 text-zinc-200 text-sm">
                                <option value="মিউজিক">মিউজিক ও গান</option>
                                <option value="টেকনোলজি">টেকনোলজি ও কোডিং</option>
                                <option value="সিনেমা ও নাটক">সিনেমা ও নাটক</option>
                                <option value="ভ্রমণ">ভ্রমণ ও প্রকৃতি</option>
                                <option value="বিনোদন">বিনোদন ও শর্টস</option>
                                <option value="শিক্ষা">শিক্ষা ও টিউটোরিয়াল</option>
                            </select>
                        </div>
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-zinc-300 mb-1" id="labelDescription">বর্ণনা</label>
                        <textarea id="uploadDesc" rows="3" placeholder="ভিডিও সম্পর্কে বিস্তারিত বিবরণ লিখুন..." class="w-full bg-zinc-900 border border-zinc-700 rounded-xl px-4 py-2.5 focus:outline-none focus:border-red-500 text-zinc-200 text-sm resize-none"></textarea>
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-zinc-300 mb-1" id="labelThumbnailUrl">থাম্বনেইল ইমেজ URL (ঐচ্ছিক)</label>
                        <input type="text" id="uploadThumb" placeholder="https://images.unsplash.com/..." class="w-full bg-zinc-900 border border-zinc-700 rounded-xl px-4 py-2.5 focus:outline-none focus:border-red-500 text-zinc-200 text-sm">
                    </div>
                </div>
            </div>

            <div class="px-6 py-4 border-t border-zinc-700 flex justify-end space-x-3 bg-zinc-900/50">
                <button onclick="closeUploadModal()" class="px-5 py-2 rounded-xl text-sm font-medium hover:bg-zinc-800 transition text-zinc-300 cursor-pointer" id="btnCancel">বাতিল</button>
                <button id="submitUploadBtn" onclick="publishVideo()" disabled class="bg-zinc-700 text-zinc-400 px-6 py-2 rounded-xl text-sm font-medium transition cursor-not-allowed">পাবলিশ করুন</button>
            </div>
        </div>
    </div>

    <!-- Create Playlist Modal -->
    <div id="playlistModal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-cardbg border border-zinc-700 w-full max-w-md rounded-2xl shadow-2xl overflow-hidden flex flex-col p-6 space-y-4">
            <div class="flex items-center justify-between border-b border-zinc-700 pb-3">
                <h3 class="font-bold text-lg text-white flex items-center space-x-2">
                    <i class="fa-solid fa-list text-emerald-400"></i>
                    <span id="plModalTitle">নতুন প্লেলিস্ট তৈরি করুন</span>
                </h3>
                <button onclick="closePlaylistModal()" class="text-zinc-400 hover:text-white p-2 cursor-pointer"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div class="space-y-3">
                <div>
                    <label class="block text-xs font-semibold text-zinc-400 mb-1" id="plNameLabel">প্লেলিস্টের নাম</label>
                    <input type="text" id="playlistNameInput" placeholder="যেমন: ফেভারিট কোডিং টিউটোরিয়াল" class="w-full bg-zinc-900 border border-zinc-700 rounded-xl px-4 py-2.5 text-sm text-zinc-100 focus:outline-none focus:border-emerald-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-zinc-400 mb-1" id="plVisLabel">দৃশ্যমানতা (Visibility)</label>
                    <select id="playlistVisSelect" class="w-full bg-zinc-900 border border-zinc-700 rounded-xl px-4 py-2.5 text-sm text-zinc-100 focus:outline-none focus:border-emerald-500">
                        <option value="public" id="optPublic">পাবলিক (Public)</option>
                        <option value="private" id="optPrivate">প্রাইভেট (Private)</option>
                    </select>
                </div>
            </div>
            <div class="flex justify-end space-x-2 pt-2">
                <button onclick="closePlaylistModal()" class="px-4 py-2 rounded-xl bg-zinc-800 text-zinc-300 text-xs font-medium cursor-pointer" id="plBtnCancel">বাতিল</button>
                <button onclick="createNewPlaylist()" class="px-5 py-2 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white text-xs font-medium cursor-pointer" id="plBtnCreate">তৈরি করুন</button>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-20 right-6 bg-zinc-800 border border-zinc-700 text-white px-5 py-3 rounded-2xl shadow-2xl z-50 transform translate-y-32 opacity-0 transition-all duration-300 flex items-center space-x-3">
        <i id="toastIcon" class="fa-solid fa-circle-check text-emerald-400 text-lg"></i>
        <span id="toastMsg" class="text-sm font-medium">সফলভাবে সম্পন্ন হয়েছে!</span>
    </div>

    <script>
        let defaultVideos = [
            {
                id: 'v1',
                title: 'সম্পূর্ণ ৫ ঘণ্টার জাভাস্ক্রিপ্ট ও রিয়্যাক্ট মাস্টারক্লাস মেগা প্রজেক্ট',
                channel: 'কোডিং গুরু বাংলাদেশ',
                avatar: 'https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=100&h=100&fit=crop',
                views: '১.২ লক্ষ',
                time: '২ দিন আগে',
                thumbnail: 'https://images.unsplash.com/photo-1555066931-4365d14bab8c?w=600&h=350&fit=crop',
                videoUrl: 'https://www.w3schools.com/html/mov_bbb.mp4',
                description: 'ফুল-স্ট্যাক ওয়েব অ্যাপ্লিকেশন তৈরির দীর্ঘ মেগা ভিডিও।',
                likes: '৮.৫ হাজার',
                category: 'টেকনোলজি',
                videoType: 'long',
                isAdult: false,
                durationSeconds: 18000,
                isSubscribed: true,
                comments: [
                    { id: 'c1', user: 'রহিম উদ্দিন', avatar: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=100&h=100&fit=crop', text: 'অসাধারণ টিউটোরিয়াল ভাই! অনেক কিছু শিখলাম।', time: '১ দিন আগে', likes: 24 }
                ]
            },
            {
                id: 'v2',
                title: '৩০ সেকেন্ডে শিখে নিন চমৎকার জাভাস্ক্রিপ্ট ট্রিক!',
                channel: 'কোডিং ট্রিকস',
                avatar: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=100&h=100&fit=crop',
                views: '৪৫ হাজার',
                time: '১ দিন আগে',
                thumbnail: 'https://images.unsplash.com/photo-1517694712202-14dd9538aa97?w=400&h=700&fit=crop',
                videoUrl: 'https://www.w3schools.com/html/mov_bbb.mp4',
                description: 'দ্রুত কোডিং সমাধান।',
                likes: '৩.২ হাজার',
                category: 'বিনোদন',
                videoType: 'short',
                isAdult: false,
                durationSeconds: 30,
                isSubscribed: true,
                comments: []
            }
        ];

        let videos = [];
        let historyList = [];
        let likedVideos = [];
        let subscriptionsList = [];
        let playlists = [
            { id: 'pl_1', name: 'আমার ফেভারিট কোডিং লিস্ট', visibility: 'public', videos: ['v1'] }
        ];
        let currentUploadType = 'long';
        let selectedFileBlob = null;
        let selectedFileDuration = 0;
        let db = null;
        let currentLanguage = 'bn';

        const translations = {
            bn: {
                appName: 'ভিডিওফ্লো প্রো',
                home: 'হোম',
                shorts: 'শর্টস',
                subscriptions: 'সাবস্ক্রিপশন',
                profile: 'প্রোফাইল',
                searchPlaceholder: 'ভিডিও বা চ্যানেল অনুসন্ধান করুন...',
                sidebarMenuTitle: 'মেনু বার',
                sidebarHome: 'হোম',
                sidebarShorts: 'শর্টস',
                sidebarSubs: 'সাবস্ক্রিপশন',
                sidebarLib: 'আপনার লাইব্রেরি',
                history: 'ইতিহাস',
                studio: 'স্টুডিও ও আপলোড',
                liked: 'পছন্দ করা ভিডিও',
                playlists: 'প্লেলিস্টসমূহ',
                sidebarExplore: 'এক্সপ্লোর ও ফিচার',
                music: 'মিউজিক ও গান',
                tech: 'গেমিং ও টেক',
                cinema: 'মুভি ও সিনেমা',
                travel: 'ভ্রমণ ও প্রকৃতি',
                sidebarFooter: 'সম্পূর্ণ ফিচার ইন্টিগ্রেটেড সংস্করণ।',
                langSettings: 'ভাষা / ল্যাঙ্গুয়েজ (Language)',
                longVideos: 'লং ভিডিওসমূহ (১৬:৯)',
                shortsFeed: 'শর্টস (৯:১৬)',
                all: 'সব',
                entertainment: 'বিনোদন',
                education: 'শিক্ষা',
                subscribe: 'সাবস্ক্রাইব',
                subscribed: 'সাবস্ক্রাইবড',
                viewsCount: 'ভিউ',
                uploadNew: 'নতুন ভিডিও আপলোড করুন',
                selectLangTitle: 'ভাষা নির্বাচন করুন (Select Language)'
            },
            en: {
                appName: 'VideoFlow Pro',
                home: 'Home',
                shorts: 'Shorts',
                subscriptions: 'Subscriptions',
                profile: 'Profile',
                searchPlaceholder: 'Search videos or channels...',
                sidebarMenuTitle: 'Menu Bar',
                sidebarHome: 'Home',
                sidebarShorts: 'Shorts',
                sidebarSubs: 'Subscriptions',
                sidebarLib: 'Your Library',
                history: 'History',
                studio: 'Studio & Upload',
                liked: 'Liked Videos',
                playlists: 'Playlists',
                sidebarExplore: 'Explore & Features',
                music: 'Music & Songs',
                tech: 'Gaming & Tech',
                cinema: 'Movies & Drama',
                travel: 'Travel & Nature',
                sidebarFooter: 'Full feature integrated version.',
                langSettings: 'Language Setting',
                longVideos: 'Long Videos (16:9)',
                shortsFeed: 'Shorts (9:16)',
                all: 'All',
                entertainment: 'Entertainment',
                education: 'Education',
                subscribe: 'Subscribe',
                subscribed: 'Subscribed',
                viewsCount: 'views',
                uploadNew: 'Upload New Video',
                selectLangTitle: 'Select Country / Language'
            },
            hi: {
                appName: 'वीडियोफ्लो प्रो',
                home: 'होम',
                shorts: 'शॉर्ट्स',
                subscriptions: 'सदस्यता',
                profile: 'प्रोफाइल',
                searchPlaceholder: 'वीडियो या चैनल खोजें...',
                sidebarMenuTitle: 'मेनू बार',
                sidebarHome: 'होम',
                sidebarShorts: 'शॉर्ट्स',
                sidebarSubs: 'सदस्यता',
                sidebarLib: 'आपकी लाइब्रेरी',
                history: 'इतिहास',
                studio: 'स्टूडियो और अपलोड',
                liked: 'पसंद किए गए वीडियो',
                playlists: 'प्लेलिस्ट',
                sidebarExplore: 'एक्सप्लोर और फीचर्स',
                music: 'संगीत और गाने',
                tech: 'गेमिंग और टेक',
                cinema: 'मूवी और सिनेमा',
                travel: 'यात्रा और प्रकृति',
                sidebarFooter: 'पूर्ण फीचर एकीकृत संस्करण।',
                langSettings: 'भाषा सेटिंग (Language)',
                longVideos: 'लंबे वीडियो (16:9)',
                shortsFeed: 'शॉर्ट्स (9:16)',
                all: 'सभी',
                entertainment: 'मनोरंजन',
                education: 'शिक्षा',
                subscribe: 'सदस्यता लें',
                subscribed: 'सदस्यता ली गई',
                viewsCount: 'व्यूज',
                uploadNew: 'नया वीडियो अपलोड करें',
                selectLangTitle: 'भाषा चुनें (Select Language)'
            },
            ar: {
                appName: 'فيديو فلو برو',
                home: 'الرئيسية',
                shorts: 'فيديوهات قصيرة',
                subscriptions: 'الاشتراكات',
                profile: 'الملف الشخصي',
                searchPlaceholder: 'البحث عن فيديوهات أو قنوات...',
                sidebarMenuTitle: 'قائمة الطعام',
                sidebarHome: 'الرئيسية',
                sidebarShorts: 'فيديوهات قصيرة',
                sidebarSubs: 'الاشتراكات',
                sidebarLib: 'مكتبتك',
                history: 'السجل',
                studio: 'الاستوديو والرفع',
                liked: 'الفيديوهات المعجب بها',
                playlists: 'قوائم التشغيل',
                sidebarExplore: 'استكشاف والمميزات',
                music: 'موسيقى وأغاني',
                tech: 'ألعاب وتقنية',
                cinema: 'أفلام ودراما',
                travel: 'سفر وطبيعة',
                sidebarFooter: 'نسخة متكاملة الميزات بالكامل.',
                langSettings: 'إعدادات اللغة (Language)',
                longVideos: 'فيديوهات طويلة (16:9)',
                shortsFeed: 'فيديوهات قصيرة (9:16)',
                all: 'الكل',
                entertainment: 'ترفيه',
                education: 'تعليم',
                subscribe: 'اشتراك',
                subscribed: 'مشترك',
                viewsCount: 'مشاهدة',
                uploadNew: 'رفع فيديو جديد',
                selectLangTitle: 'اختر لغة البلد (Select Language)'
            }
        };

        const availableLanguages = [
            { code: 'bn', name: 'বাংলা (Bangladesh)', flag: '🇧🇩' },
            { code: 'en', name: 'English (United States / UK)', flag: '🇺🇸' },
            { code: 'hi', name: 'हिन्दी (India)', flag: '🇮🇳' },
            { code: 'ar', name: 'العربية (Saudi Arabia / UAE)', flag: '🇸🇦' }
        ];

        window.onload = function() {
            initIndexedDB();
            initAutoHideNavbar();
        };

        function openLanguageModal() {
            const container = document.getElementById('languageListContainer');
            container.innerHTML = availableLanguages.map(lang => `
                <div onclick="setAppLanguage('${lang.code}')" class="flex items-center justify-between p-3.5 rounded-xl hover:bg-hoverbg cursor-pointer transition border ${currentLanguage === lang.code ? 'border-red-500 bg-red-500/10' : 'border-zinc-800 bg-zinc-900/60'}">
                    <div class="flex items-center space-x-3">
                        <span class="text-2xl">${lang.flag}</span>
                        <span class="font-semibold text-sm text-zinc-100">${lang.name}</span>
                    </div>
                    ${currentLanguage === lang.code ? '<i class="fa-solid fa-check text-red-500 text-lg"></i>' : ''}
                </div>
            `).join('');
            document.getElementById('languageModal').classList.remove('hidden');
        }

        function closeLanguageModal() {
            document.getElementById('languageModal').classList.add('hidden');
        }

        function setAppLanguage(langCode) {
            currentLanguage = langCode;
            closeLanguageModal();
            updateUILabels();
            showToast('ভাষা সফলভাবে পরিবর্তন করা হয়েছে!');
            switchTab('profile');
        }

        function updateUILabels() {
            const t = translations[currentLanguage];
            document.getElementById('bottomNavHome').innerText = t.home;
            document.getElementById('bottomNavShorts').innerText = t.shorts;
            document.getElementById('bottomNavSubs').innerText = t.subscriptions;
            document.getElementById('navProfileText').innerText = t.profile;
            
            // Sidebar updates
            document.getElementById('sidebarMenuTitle').innerText = t.sidebarMenuTitle;
            document.getElementById('sidebarHome').innerText = t.sidebarHome;
            document.getElementById('sidebarShorts').innerText = t.sidebarShorts;
            document.getElementById('sidebarSubs').innerText = t.sidebarSubs;
            document.getElementById('sidebarLibTitle').innerText = t.sidebarLib;
            document.getElementById('sidebarHistory').innerText = t.history;
            document.getElementById('sidebarStudio').innerText = t.studio;
            document.getElementById('sidebarLiked').innerText = t.liked;
            document.getElementById('sidebarPlaylists').innerText = t.playlists;
            document.getElementById('sidebarExploreTitle').innerText = t.sidebarExplore;
            document.getElementById('expMusic').innerText = t.music;
            document.getElementById('expTech').innerText = t.tech;
            document.getElementById('expCinema').innerText = t.cinema;
            document.getElementById('expTravel').innerText = t.travel;
            document.getElementById('sidebarFooterDesc').innerText = t.sidebarFooter;

            document.getElementById('searchInput').placeholder = t.searchPlaceholder;
        }

        function initAutoHideNavbar() {
            let touchStartY = 0;
            const navBar = document.getElementById('bottomNavBar');
            const gestureArea = document.getElementById('bottomGestureArea');

            window.addEventListener('touchstart', function(e) {
                touchStartY = e.touches[0].clientY;
            }, { passive: true });

            window.addEventListener('touchend', function(e) {
                let touchEndY = e.changedTouches[0].clientY;
                if (touchStartY > window.innerHeight - 80 && (touchStartY - touchEndY) > 25) {
                    navBar.classList.remove('nav-hidden');
                }
            }, { passive: true });

            if (gestureArea) {
                gestureArea.addEventListener('click', function() {
                    navBar.classList.toggle('nav-hidden');
                });
                gestureArea.addEventListener('touchend', function() {
                    navBar.classList.remove('nav-hidden');
                });
            }
        }

        function initIndexedDB() {
            const request = indexedDB.open('VideoFlowProDB', 11);
            request.onerror = () => initLocalStorageFallback();
            request.onupgradeneeded = (event) => {
                db = event.target.result;
                if (!db.objectStoreNames.contains('videos')) db.createObjectStore('videos', { keyPath: 'id' });
                if (!db.objectStoreNames.contains('userdata')) db.createObjectStore('userdata', { keyPath: 'key' });
            };
            request.onsuccess = (event) => {
                db = event.target.result;
                loadAllDataFromDB();
            };
        }

        function initLocalStorageFallback() {
            videos = defaultVideos;
            updateSubscriptionsList();
            switchTab('home');
        }

        function loadAllDataFromDB() {
            if (!db) {
                initLocalStorageFallback();
                return;
            }
            const transaction = db.transaction(['videos', 'userdata'], 'readonly');
            const videoReq = transaction.objectStore('videos').getAll();

            videoReq.onsuccess = function() {
                if (videoReq.result && videoReq.result.length > 0) {
                    videos = videoReq.result;
                } else {
                    videos = defaultVideos;
                }
                loadUserData();
            };
            videoReq.onerror = function() {
                videos = defaultVideos;
                loadUserData();
            };
        }

        function loadUserData() {
            if (!db) return;
            const transaction = db.transaction(['userdata'], 'readonly');
            const store = transaction.objectStore('userdata');
            store.get('history').onsuccess = (e) => { if (e.target.result) historyList = e.target.result.value; };
            store.get('liked').onsuccess = (e) => { if (e.target.result) likedVideos = e.target.result.value; };
            store.get('playlists').onsuccess = (e) => { if (e.target.result) playlists = e.target.result.value; };
            updateSubscriptionsList();
            switchTab('home');
        }

        function saveUserDataToDB() {
            if (!db) return;
            try {
                const transaction = db.transaction(['userdata'], 'readwrite');
                const store = transaction.objectStore('userdata');
                store.put({ key: 'history', value: historyList });
                store.put({ key: 'liked', value: likedVideos });
                store.put({ key: 'playlists', value: playlists });
            } catch(err) {
                console.error(err);
            }
        }

        function updateSubscriptionsList() {
            subscriptionsList = videos.filter(v => v.isSubscribed);
        }

        function toggleSidebar() {
            const sidebar = document.getElementById('sidebar');
            const backdrop = document.getElementById('sidebarBackdrop');
            sidebar.classList.toggle('-translate-x-full');
            backdrop.classList.toggle('hidden');
        }

        function toggleSidebarMobileOnly() {
            if (window.innerWidth < 1024) toggleSidebar();
        }

        function toggleSearchModal() {
            document.getElementById('searchModal').classList.toggle('hidden');
        }

        function openNotificationsModal() {
            document.getElementById('notificationsModal').classList.remove('hidden');
        }

        function closeNotificationsModal() {
            document.getElementById('notificationsModal').classList.add('hidden');
        }

        function openUploadModal() {
            document.getElementById('uploadModal').classList.remove('hidden');
            document.getElementById('uploadProgressContainer').classList.add('hidden');
            document.getElementById('uploadFormFields').classList.add('hidden');
            document.getElementById('submitUploadBtn').disabled = true;
            document.getElementById('submitUploadBtn').className = "bg-zinc-700 text-zinc-400 px-6 py-2 rounded-xl text-sm font-medium transition cursor-not-allowed";
        }

        function closeUploadModal() {
            document.getElementById('uploadModal').classList.add('hidden');
            selectedFileBlob = null;
        }

        function setVideoType(type) {
            currentUploadType = type;
            const longBtn = document.getElementById('typeLongBtn');
            const shortBtn = document.getElementById('typeShortBtn');
            if (type === 'long') {
                longBtn.className = "p-4 rounded-xl border-2 border-red-500 bg-red-500/10 text-left transition flex items-center space-x-3 cursor-pointer";
                shortBtn.className = "p-4 rounded-xl border-2 border-zinc-700 bg-zinc-900 text-left transition flex items-center space-x-3 cursor-pointer";
            } else {
                shortBtn.className = "p-4 rounded-xl border-2 border-yellow-500 bg-yellow-500/10 text-left transition flex items-center space-x-3 cursor-pointer";
                longBtn.className = "p-4 rounded-xl border-2 border-zinc-700 bg-zinc-900 text-left transition flex items-center space-x-3 cursor-pointer";
            }
        }

        function handleFileSelect(event) {
            const file = event.target.files[0];
            if (!file) return;

            const fileNameLower = file.name.toLowerCase();
            const forbiddenKeywords = ['porn', 'xxx', 'bad18', 'nude', 'adult_explicit_block'];
            const mildKeywords = ['swim', 'beach', 'fashion', 'model', 'soft'];

            let isBlocked = forbiddenKeywords.some(keyword => fileNameLower.includes(keyword));
            let isAuto18Plus = mildKeywords.some(keyword => fileNameLower.includes(keyword));

            if (isBlocked) {
                showToast('অ্যালগরিদম স্ক্যান: এই ভিডিওটিতে অত্যন্ত ক্ষতিকর উপাদান পাওয়ায় আপলোড ব্লক করা হয়েছে!', 'error');
                event.target.value = '';
                return;
            }

            selectedFileBlob = file;
            document.getElementById('selectedFileName').innerText = file.name;
            
            const videoElem = document.createElement('video');
            videoElem.preload = 'metadata';
            videoElem.onloadedmetadata = function() {
                window.URL.revokeObjectURL(videoElem.src);
                selectedFileDuration = videoElem.duration || 120;
            }
            videoElem.src = URL.createObjectURL(file);

            const progressContainer = document.getElementById('uploadProgressContainer');
            const progressBarFill = document.getElementById('progressBarFill');
            const progressPercent = document.getElementById('progressPercent');
            const progressStatusText = document.getElementById('progressStatusText');
            
            progressContainer.classList.remove('hidden');
            progressBarFill.style.width = '0%';
            progressPercent.innerText = '০%';

            let progress = 0;
            const interval = setInterval(() => {
                progress += 25;
                progressBarFill.style.width = progress + '%';
                progressPercent.innerText = progress + '%';

                if (progress === 50) {
                    progressStatusText.innerText = "ব্রাউজার এআই অ্যালগরিদম স্ক্যানিং ও সেফটি চেকিং...";
                }

                if (progress >= 100) {
                    clearInterval(interval);
                    progressContainer.classList.add('hidden');
                    document.getElementById('uploadFormFields').classList.remove('hidden');
                    const submitBtn = document.getElementById('submitUploadBtn');
                    submitBtn.disabled = false;
                    submitBtn.className = "bg-red-600 hover:bg-red-700 text-white px-6 py-2 rounded-xl text-sm font-medium transition shadow-lg shadow-red-600/30 cursor-pointer";
                    
                    const baseTitle = file.name.substring(0, file.name.lastIndexOf('.')) || file.name;
                    document.getElementById('uploadTitle').value = baseTitle;

                    if (isAuto18Plus) {
                        showToast('সতর্কতা: অ্যালগরিদম ভিডিওটি কিছুটা সংবেদনশীল বা হালকা অশালীন পাওয়ায় স্বয়ংক্রিয়ভাবে 18+ রেস্ট্রিক্টেড করা হয়েছে।');
                        window.tempDetected18Plus = true;
                    } else {
                        window.tempDetected18Plus = false;
                        showToast('ফাইল সফলভাবে স্ক্যান ও অনুমোদিত হয়েছে!');
                    }
                }
            }, 300);
        }

        function switchTab(tab, category = null) {
            ['home', 'shorts', 'subscriptions', 'profile'].forEach(t => {
                const el = document.getElementById('nav-' + t);
                if (el) {
                    if (t === tab) {
                        el.className = "flex flex-col items-center space-y-1 text-red-500 transition group font-bold py-1";
                        el.querySelector('i').classList.add('text-red-500');
                    } else {
                        el.className = "flex flex-col items-center space-y-1 text-zinc-400 hover:text-white transition group py-1";
                        el.querySelector('i').classList.remove('text-red-500');
                    }
                }
            });

            const main = document.getElementById('mainContent');
            if (tab === 'home') renderHomeFeed(main, category);
            else if (tab === 'shorts') renderShortsFeed(main);
            else if (tab === 'subscriptions') renderSubscriptionsFeed(main);
            else if (tab === 'history') renderListView(main, historyList, 'দেখার ইতিহাস', 'আপনার দেখা ভিডিওগুলো।');
            else if (tab === 'liked') renderListView(main, likedVideos, 'পছন্দ করা ভিডিও', 'আপনার লাইক করা ভিডিওসমূহ।');
            else if (tab === 'playlists') renderPlaylistsView(main);
            else if (tab === 'profile') renderProfilePageView(main);
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function formatDuration(seconds) {
            if (!seconds || isNaN(seconds)) return '০:০০';
            const hrs = Math.floor(seconds / 3600);
            const mins = Math.floor((seconds % 3600) / 60);
            const secs = Math.floor(seconds % 60);
            if (hrs > 0) {
                return `${hrs}:${mins < 10 ? '0' : ''}${mins}:${secs < 10 ? '0' : ''}${secs}`;
            }
            return `${mins}:${secs < 10 ? '0' : ''}${secs}`;
        }

        function renderListView(container, items, title, subtitle) {
            container.innerHTML = `
                <div class="max-w-4xl mx-auto space-y-4">
                    <h1 class="text-2xl font-bold">${title}</h1>
                    <p class="text-xs text-zinc-400">${subtitle}</p>
                    ${items.length === 0 ? `
                        <div class="text-center py-16 bg-cardbg border border-zinc-800 rounded-2xl">
                            <i class="fa-solid fa-folder-open text-4xl text-zinc-600 mb-3"></i>
                            <h3 class="font-bold text-lg">কোনো তথ্য পাওয়া যায়নি</h3>
                        </div>
                    ` : `
                        <div class="space-y-3">
                            ${items.map(v => `
                                <div class="flex gap-4 bg-cardbg border border-zinc-800 p-4 rounded-2xl cursor-pointer hover:border-zinc-700 transition" onclick="playVideo('${v.id}')">
                                    <img src="${v.thumbnail}" class="w-36 aspect-video rounded-xl object-cover bg-zinc-900">
                                    <div class="flex-1">
                                        <h3 class="font-bold text-sm text-zinc-100">${v.title}</h3>
                                        <p class="text-xs text-zinc-400 mt-1">${v.channel} • ${formatDuration(v.durationSeconds)}</p>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                    `}
                </div>
            `;
        }

        function renderPlaylistsView(container) {
            container.innerHTML = `
                <div class="max-w-5xl mx-auto space-y-6">
                    <div class="flex items-center justify-between bg-cardbg border border-zinc-800 p-6 rounded-2xl shadow-lg">
                        <div>
                            <h1 class="text-2xl font-bold flex items-center space-x-2">
                                <i class="fa-solid fa-list text-emerald-400"></i>
                                <span>আপনার প্লেলিস্টসমূহ</span>
                            </h1>
                            <p class="text-sm text-zinc-400 mt-1">আপনার তৈরি করা সমস্ত প্লেলিস্ট এখানে সংরক্ষিত আছে।</p>
                        </div>
                        <button onclick="openPlaylistModal()" class="bg-emerald-600 hover:bg-emerald-700 text-white px-5 py-2.5 rounded-xl font-medium text-sm transition shadow-lg cursor-pointer">নতুন প্লেলিস্ট</button>
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5">
                        ${playlists.map(pl => {
                            const firstVid = videos.find(v => pl.videos && pl.videos.includes(v.id));
                            const thumb = firstVid ? firstVid.thumbnail : 'https://images.unsplash.com/photo-1555066931-4365d14bab8c?w=600&h=350&fit=crop';
                            return `
                                <div class="bg-cardbg border border-zinc-800 rounded-2xl overflow-hidden p-4 space-y-3 flex flex-col justify-between shadow-md">
                                    <div class="relative w-full aspect-video rounded-xl overflow-hidden bg-zinc-900">
                                        <img src="${thumb}" class="w-full h-full object-cover">
                                        <div class="absolute bottom-2 right-2 bg-black/80 px-2 py-0.5 rounded text-[11px] font-bold text-white">${pl.videos ? pl.videos.length : 0} ভিডিও</div>
                                    </div>
                                    <div>
                                        <h3 class="font-bold text-base text-zinc-100">${pl.name}</h3>
                                        <p class="text-xs text-zinc-400 mt-0.5">Visibility: ${pl.visibility}</p>
                                    </div>
                                    <div class="flex justify-end space-x-2 pt-2 border-t border-zinc-800">
                                        <button onclick="deletePlaylist('${pl.id}')" class="text-red-400 hover:text-red-300 text-xs font-medium cursor-pointer py-1 px-3 bg-red-500/10 rounded-lg">মুছে ফেলুন</button>
                                    </div>
                                </div>
                            `;
                        }).join('')}
                    </div>
                </div>
            `;
        }

        function openPlaylistModal() {
            document.getElementById('playlistModal').classList.remove('hidden');
        }

        function closePlaylistModal() {
            document.getElementById('playlistModal').classList.add('hidden');
        }

        function createNewPlaylist() {
            const name = document.getElementById('playlistNameInput').value.trim();
            const vis = document.getElementById('playlistVisSelect').value;
            if (!name) {
                showToast('প্লেলিস্টের নাম দিন।', 'error');
                return;
            }
            playlists.push({
                id: 'pl_' + Date.now(),
                name: name,
                visibility: vis,
                videos: []
            });
            saveUserDataToDB();
            closePlaylistModal();
            showToast('প্লেলিস্ট সফলভাবে তৈরি হয়েছে!');
            switchTab('playlists');
        }

        function deletePlaylist(id) {
            playlists = playlists.filter(pl => pl.id !== id);
            saveUserDataToDB();
            showToast('প্লেলিস্ট মুছে ফেলা হয়েছে।');
            switchTab('playlists');
        }

        function renderProfilePageView(container) {
            container.innerHTML = `
                <div class="max-w-2xl mx-auto space-y-6 pb-12">
                    <div class="flex items-center justify-between px-2">
                        <div class="flex items-center space-x-4">
                            <img src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=200&h=200&fit=crop" class="w-16 h-16 rounded-full object-cover border-2 border-zinc-700 shadow-md">
                            <div>
                                <h1 class="text-xl font-bold text-white leading-tight">Fact Bangla</h1>
                                <p class="text-xs text-zinc-400 mt-0.5">@StoryVerseAny</p>
                            </div>
                        </div>
                        <button onclick="openLanguageModal()" class="w-10 h-10 rounded-full hover:bg-hoverbg flex items-center justify-center text-zinc-200 transition bg-zinc-800/80 border border-zinc-700 cursor-pointer" title="ভাষা ও সেটিংস">
                            <i class="fa-solid fa-gear text-lg text-emerald-400"></i>
                        </button>
                    </div>

                    <div class="grid grid-cols-2 gap-3 px-2">
                        <button onclick="renderChannelPageView()" class="bg-zinc-800 hover:bg-zinc-700 text-white font-medium py-2.5 px-4 rounded-full text-xs transition border border-zinc-700/60 text-center cursor-pointer">View channel</button>
                        <button onclick="showToast('Get Premium feature activated!')" class="bg-zinc-800 hover:bg-zinc-700 text-white font-medium py-2.5 px-4 rounded-full text-xs transition border border-zinc-700/60 text-center cursor-pointer">Get Premium</button>
                    </div>

                    <div class="space-y-3 pt-2">
                        <div class="flex items-center justify-between px-2 cursor-pointer" onclick="switchTab('history')">
                            <h2 class="text-lg font-bold text-white flex items-center space-x-1">
                                <span>History</span>
                                <i class="fa-solid fa-chevron-right text-xs text-zinc-400"></i>
                            </h2>
                        </div>
                        <div class="flex space-x-3 overflow-x-auto pb-2 scrollbar-none px-2">
                            ${historyList.length === 0 ? `
                                <div class="text-xs text-zinc-500 py-4 px-2">কোনো দেখার ইতিহাস নেই।</div>
                            ` : historyList.map(v => `
                                <div class="flex flex-col shrink-0 w-40 cursor-pointer group" onclick="playVideo('${v.id}')">
                                    <div class="relative w-full aspect-video bg-zinc-900 rounded-xl overflow-hidden border border-zinc-800">
                                        <img src="${v.thumbnail}" class="w-full h-full object-cover group-hover:scale-105 transition">
                                        <div class="absolute bottom-1 right-1 bg-black/80 text-[10px] px-1.5 py-0.5 rounded text-zinc-200">${formatDuration(v.durationSeconds)}</div>
                                    </div>
                                    <h4 class="text-xs font-medium text-zinc-200 line-clamp-2 mt-1.5 leading-snug">${v.title}</h4>
                                    <p class="text-[11px] text-zinc-500 truncate mt-0.5">${v.channel}</p>
                                </div>
                            `).join('')}
                        </div>
                    </div>

                    <div class="space-y-4 pt-2">
                        <div class="flex items-center justify-between px-2">
                            <h2 class="text-lg font-bold text-white">Library</h2>
                        </div>
                        <div class="space-y-1 px-1">
                            <div onclick="switchTab('liked')" class="flex items-center space-x-4 p-3 hover:bg-zinc-900/60 rounded-2xl cursor-pointer transition">
                                <div class="w-20 aspect-video rounded-xl bg-zinc-800 overflow-hidden relative border border-zinc-700/60">
                                    <img src="${likedVideos.length > 0 ? likedVideos[0].thumbnail : 'https://images.unsplash.com/photo-1555066931-4365d14bab8c?w=200&h=120&fit=crop'}" class="w-full h-full object-cover">
                                    <div class="absolute inset-0 bg-black/30 flex items-center justify-center text-white text-xs"><i class="fa-solid fa-thumbs-up"></i></div>
                                </div>
                                <div class="flex-1">
                                    <h4 class="font-bold text-sm text-zinc-100">Liked videos</h4>
                                    <p class="text-xs text-zinc-400">Private • ${likedVideos.length} videos</p>
                                </div>
                            </div>
                            <div onclick="switchTab('playlists')" class="flex items-center space-x-4 p-3 hover:bg-zinc-900/60 rounded-2xl cursor-pointer transition">
                                <div class="w-20 aspect-video rounded-xl bg-zinc-800 overflow-hidden relative border border-zinc-700/60">
                                    <img src="https://images.unsplash.com/photo-1517694712202-14dd9538aa97?w=200&h=120&fit=crop" class="w-full h-full object-cover">
                                    <div class="absolute inset-0 bg-black/30 flex items-center justify-center text-white text-xs"><i class="fa-solid fa-list"></i></div>
                                </div>
                                <div class="flex-1">
                                    <h4 class="font-bold text-sm text-zinc-100">Playlists</h4>
                                    <p class="text-xs text-zinc-400">${playlists.length} playlists created</p>
                                </div>
                            </div>
                            <div onclick="openStudio()" class="flex items-center space-x-4 p-3 hover:bg-zinc-900/60 rounded-2xl cursor-pointer transition">
                                <div class="w-20 aspect-video rounded-xl bg-zinc-800 overflow-hidden relative border border-zinc-700/60">
                                    <img src="${videos.length > 0 ? videos[0].thumbnail : 'https://images.unsplash.com/photo-1555066931-4365d14bab8c?w=200&h=120&fit=crop'}" class="w-full h-full object-cover">
                                    <div class="absolute inset-0 bg-black/30 flex items-center justify-center text-white text-xs"><i class="fa-solid fa-clapperboard"></i></div>
                                </div>
                                <div class="flex-1">
                                    <h4 class="font-bold text-sm text-zinc-100">Your videos</h4>
                                    <p class="text-xs text-zinc-400">${videos.length} videos uploaded</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            `;
        }

        function renderHomeFeed(container, activeCategory = null) {
            const t = translations[currentLanguage];
            const categories = [t.all, t.music, t.tech, t.cinema, t.travel, t.entertainment, t.education];
            const rawCategories = ['সব', 'মিউজিক', 'টেকনোলজি', 'সিনেমা ও নাটক', 'ভ্রমণ', 'বিনোদন', 'শিক্ষা'];
            
            let activeRaw = 'সব';
            if (activeCategory) {
                const idx = categories.indexOf(activeCategory);
                if (idx !== -1) activeRaw = rawCategories[idx];
                else activeRaw = activeCategory;
            }

            const displayVideos = activeRaw !== 'সব' ? videos.filter(v => v.category === activeRaw) : videos;
            const shortsList = videos.filter(v => v.videoType === 'short');
            const longList = displayVideos.filter(v => v.videoType !== 'short');

            container.innerHTML = `
                <div class="mb-4 flex items-center space-x-2 overflow-x-auto pb-2 scrollbar-none">
                    ${categories.map((cat, idx) => `
                        <button onclick="switchTab('home', '${cat}')" class="px-4 py-1.5 rounded-lg text-sm font-medium whitespace-nowrap transition cursor-pointer ${(!activeCategory && idx === 0) || activeCategory === cat ? 'bg-white text-black shadow' : 'bg-zinc-800 hover:bg-zinc-700 text-zinc-300'}">${cat}</button>
                    `).join('')}
                </div>

                <div class="mb-8">
                    <div class="flex items-center justify-between mb-4">
                        <h2 class="text-xl font-bold flex items-center space-x-2">
                            <i class="fa-solid fa-film text-red-500"></i>
                            <span>${activeRaw !== 'সব' ? activeRaw + ' ভিডিওসমূহ' : t.longVideos}</span>
                        </h2>
                    </div>
                    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-5">
                        ${longList.map(v => `
                            <div class="flex flex-col group cursor-pointer" onclick="playVideo('${v.id}')">
                                <div class="relative w-full long-card-aspect rounded-2xl overflow-hidden bg-zinc-900 shadow-md border border-zinc-800/60">
                                    <img src="${v.thumbnail}" class="w-full h-full object-cover group-hover:scale-105 transition duration-300">
                                    <div class="absolute bottom-2 right-2 bg-black/85 text-[11px] px-2 py-0.5 rounded font-semibold text-zinc-200">${formatDuration(v.durationSeconds)}</div>
                                    ${v.isAdult ? '<div class="absolute top-2 left-2 bg-rose-600 text-white text-[10px] px-2 py-0.5 rounded font-bold">18+</div>' : ''}
                                </div>
                                <div class="flex mt-3 space-x-3">
                                    <img src="${v.avatar}" class="w-9 h-9 rounded-full object-cover shrink-0">
                                    <div class="flex-1 overflow-hidden">
                                        <h3 class="font-semibold text-sm line-clamp-2 text-zinc-100 group-hover:text-red-400 transition leading-snug">${v.title}</h3>
                                        <p class="text-xs text-zinc-400 mt-1">${v.channel}</p>
                                        <p class="text-xs text-zinc-500">${v.views} ${t.viewsCount}</p>
                                    </div>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>

                ${shortsList.length > 0 && activeRaw === 'সব' ? `
                    <div class="mb-8 pt-4 border-t border-zinc-800">
                        <div class="flex items-center justify-between mb-4">
                            <h2 class="text-xl font-bold flex items-center space-x-2">
                                <i class="fa-solid fa-bolt text-yellow-500"></i>
                                <span>${t.shortsFeed}</span>
                            </h2>
                        </div>
                        <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-6 gap-4">
                            ${shortsList.map(s => `
                                <div class="flex flex-col group cursor-pointer" onclick="playVideo('${s.id}')">
                                    <div class="relative w-full short-card-aspect rounded-2xl overflow-hidden bg-zinc-900 shadow-lg border border-zinc-800">
                                        <img src="${s.thumbnail}" class="w-full h-full object-cover group-hover:scale-105 transition duration-300">
                                        <div class="absolute bottom-2 right-2 bg-black/85 text-[10px] px-1.5 py-0.5 rounded font-bold text-zinc-200">${formatDuration(s.durationSeconds)}</div>
                                        ${s.isAdult ? '<div class="absolute top-2 left-2 bg-rose-600 text-white text-[9px] px-1.5 py-0.5 rounded font-bold">18+</div>' : ''}
                                        <div class="absolute inset-x-0 bottom-0 bg-gradient-to-t from-black/80 to-transparent p-3">
                                            <h4 class="font-bold text-xs line-clamp-2 text-white">${s.title}</h4>
                                        </div>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                ` : ''}
            `;
        }

        function renderShortsFeed(container) {
            const shorts = videos.filter(v => v.videoType === 'short');
            container.innerHTML = `
                <div class="max-w-xl mx-auto space-y-6">
                    <h1 class="text-2xl font-bold flex items-center space-x-2">
                        <i class="fa-solid fa-bolt text-yellow-500"></i>
                        <span>শর্টস ফিড (৯:১৬)</span>
                    </h1>
                    ${shorts.map(s => `
                        <div class="bg-cardbg border border-zinc-800 rounded-3xl overflow-hidden shadow-2xl p-4 space-y-3">
                            <div class="flex items-center justify-between">
                                <div class="flex items-center space-x-3">
                                    <img src="${s.avatar}" class="w-9 h-9 rounded-full object-cover">
                                    <div>
                                        <h4 class="font-bold text-sm">${s.channel}</h4>
                                        ${s.isAdult ? '<span class="text-[10px] bg-rose-500/20 text-rose-400 px-2 py-0.5 rounded font-bold">18+ Restricted</span>' : ''}
                                    </div>
                                </div>
                            </div>
                            <div class="w-full max-w-sm mx-auto short-card-aspect bg-black rounded-2xl overflow-hidden relative flex items-center justify-center">
                                <video src="${s.videoBlob ? URL.createObjectURL(s.videoBlob) : s.videoUrl}" controls autoplay loop class="w-full h-full object-cover"></video>
                            </div>
                            <h3 class="font-bold text-base text-zinc-100">${s.title}</h3>
                        </div>
                    `).join('')}
                </div>
            `;
        }

        function renderSubscriptionsFeed(container) {
            container.innerHTML = `
                <div class="max-w-7xl mx-auto space-y-6">
                    <div class="flex items-center justify-between bg-cardbg border border-zinc-800 p-6 rounded-2xl">
                        <div>
                            <h1 class="text-2xl font-bold flex items-center space-x-2">
                                <i class="fa-solid fa-users text-blue-500"></i>
                                <span>সাবস্ক্রিপশন ফিড</span>
                            </h1>
                            <p class="text-sm text-zinc-400 mt-1">যাদের চ্যানেল আপনি সাবস্ক্রাইব করেছেন তাদের সর্বশেষ ভিডিওসমূহ।</p>
                        </div>
                    </div>
                    ${subscriptionsList.length === 0 ? `
                        <div class="text-center py-16 bg-cardbg border border-zinc-800 rounded-2xl">
                            <i class="fa-solid fa-user-slash text-4xl text-zinc-600 mb-3"></i>
                            <h3 class="font-bold text-lg">কোনো সাবস্ক্রাইব করা চ্যানেল নেই</h3>
                        </div>
                    ` : `
                        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-5">
                            ${subscriptionsList.map(v => `
                                <div class="flex flex-col group cursor-pointer" onclick="playVideo('${v.id}')">
                                    <div class="relative w-full long-card-aspect rounded-2xl overflow-hidden bg-zinc-900 shadow-md border border-zinc-800">
                                        <img src="${v.thumbnail}" class="w-full h-full object-cover group-hover:scale-105 transition duration-300">
                                        <div class="absolute bottom-2 right-2 bg-black/85 text-[11px] px-2 py-0.5 rounded font-semibold text-zinc-200">${formatDuration(v.durationSeconds)}</div>
                                    </div>
                                    <div class="flex mt-3 space-x-3">
                                        <img src="${v.avatar}" class="w-9 h-9 rounded-full object-cover shrink-0">
                                        <div class="flex-1 overflow-hidden">
                                            <h3 class="font-semibold text-sm line-clamp-2 text-zinc-100 group-hover:text-red-400 transition leading-snug">${v.title}</h3>
                                            <p class="text-xs text-zinc-400 mt-1">${v.channel}</p>
                                        </div>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                    `}
                </div>
            `;
        }

        function renderChannelPageView() {
            const main = document.getElementById('mainContent');
            main.innerHTML = `
                <div class="max-w-4xl mx-auto pb-16 relative">
                    <div class="absolute top-2 left-2 z-20">
                        <button onclick="switchTab('profile')" class="w-10 h-10 rounded-full bg-black/60 backdrop-blur text-white flex items-center justify-center hover:bg-black/80 transition shadow-lg cursor-pointer" title="ফিরে যান">
                            <i class="fa-solid fa-arrow-left text-lg"></i>
                        </button>
                    </div>

                    <div class="w-full h-36 sm:h-48 bg-zinc-900 overflow-hidden relative rounded-2xl border border-zinc-800">
                        <img src="https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?w=1200&h=400&fit=crop" class="w-full h-full object-cover">
                    </div>

                    <div class="px-4 pt-4 space-y-4">
                        <div class="flex items-start space-x-4">
                            <img src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=200&h=200&fit=crop" class="w-20 h-20 sm:w-24 sm:h-24 rounded-full object-cover border-4 border-darkbg -mt-10 sm:-mt-12 relative z-10 shadow-xl">
                            <div class="flex-1 pt-1">
                                <h1 class="text-xl sm:text-2xl font-bold text-white">Fact Bangla</h1>
                                <p class="text-xs sm:text-sm text-zinc-400">@StoryVerseAny</p>
                            </div>
                        </div>

                        <div class="grid grid-cols-2 gap-3 pt-1">
                            <button onclick="openStudio()" class="bg-zinc-800 hover:bg-zinc-700 text-white font-medium py-2.5 px-4 rounded-full text-xs transition border border-zinc-700 text-center flex items-center justify-center space-x-2 cursor-pointer">
                                <i class="fa-solid fa-chart-bar text-zinc-400"></i>
                                <span>Analytics</span>
                            </button>
                            <button onclick="openStudio()" class="bg-zinc-800 hover:bg-zinc-700 text-white font-medium py-2.5 px-4 rounded-full text-xs transition border border-zinc-700 text-center flex items-center justify-center space-x-2 cursor-pointer">
                                <i class="fa-solid fa-pen text-zinc-400"></i>
                                <span>Edit channel</span>
                            </button>
                        </div>

                        <div class="space-y-3 pt-4">
                            <h2 class="text-base sm:text-lg font-bold text-white">Videos</h2>
                            <div class="space-y-3">
                                ${videos.map(v => `
                                    <div class="flex space-x-3 cursor-pointer group" onclick="playVideo('${v.id}')">
                                        <img src="${v.thumbnail}" class="w-32 aspect-video rounded-xl object-cover bg-zinc-900 shrink-0">
                                        <div class="flex-1">
                                            <h4 class="text-xs sm:text-sm font-semibold text-zinc-100 line-clamp-2 leading-snug">${v.title}</h4>
                                            <p class="text-[11px] text-zinc-500 mt-1">${v.views} views • ${v.time}</p>
                                        </div>
                                    </div>
                                `).join('')}
                            </div>
                        </div>
                    </div>
                </div>
            `;
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function playVideo(id) {
            const v = videos.find(x => x.id === id);
            if (!v) return;
            const t = translations[currentLanguage];

            if (!historyList.some(item => item.id === v.id)) {
                historyList.unshift(v);
                saveUserDataToDB();
            }

            const main = document.getElementById('mainContent');
            const isLiked = likedVideos.some(item => item.id === v.id);
            const playbackSource = v.videoBlob ? URL.createObjectURL(v.videoBlob) : v.videoUrl;
            const isShort = v.videoType === 'short';

            main.innerHTML = `
                <div class="max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-3 gap-6">
                    <div class="lg:col-span-2 space-y-4">
                        <div class="w-full ${isShort ? 'max-w-md mx-auto short-card-aspect' : 'aspect-video'} bg-black rounded-2xl overflow-hidden shadow-2xl relative border border-zinc-800 flex items-center justify-center">
                            <video src="${playbackSource}" controls autoplay class="w-full h-full ${isShort ? 'object-cover' : 'object-contain'}"></video>
                        </div>
                        <div class="flex items-center space-x-2">
                            <span class="text-xs ${isShort ? 'bg-yellow-500 text-black' : 'bg-red-600 text-white'} px-2.5 py-0.5 rounded font-bold">${isShort ? '৯:১৬ শর্ট' : '১৬:৯ লং'}</span>
                            ${v.isAdult ? '<span class="text-xs bg-rose-600 text-white px-2.5 py-0.5 rounded font-bold">18+ Restricted</span>' : ''}
                        </div>
                        <h1 class="text-xl font-bold text-zinc-100 leading-snug">${v.title}</h1>
                        <div class="flex flex-wrap items-center justify-between gap-4 border-b border-zinc-800 pb-4">
                            <div class="flex items-center space-x-3">
                                <img src="${v.avatar}" class="w-11 h-11 rounded-full object-cover">
                                <div>
                                    <h3 class="font-bold text-sm text-zinc-200">${v.channel}</h3>
                                </div>
                                <button onclick="toggleSubscribe('${v.id}')" class="px-4 py-1.5 rounded-full text-xs font-semibold transition cursor-pointer ${v.isSubscribed ? 'bg-zinc-800 text-zinc-300 hover:bg-zinc-700' : 'bg-white text-black hover:bg-zinc-200'}">
                                    ${v.isSubscribed ? t.subscribed : t.subscribe}
                                </button>
                            </div>
                            <div class="flex items-center space-x-2 bg-zinc-900 border border-zinc-700/60 rounded-full p-1">
                                <button onclick="toggleLike('${v.id}')" class="flex items-center space-x-2 px-4 py-1.5 hover:bg-zinc-800 rounded-full text-sm font-medium transition cursor-pointer ${isLiked ? 'text-red-500 font-bold' : ''}">
                                    <i class="${isLiked ? 'fa-solid' : 'fa-regular'} fa-thumbs-up"></i>
                                    <span>${v.likes}</span>
                                </button>
                            </div>
                        </div>
                        <div class="bg-zinc-900/80 border border-zinc-800 rounded-2xl p-4 text-sm space-y-2">
                            <p class="text-zinc-300 whitespace-pre-line leading-relaxed">${v.description}</p>
                        </div>

                        <!-- Comment System -->
                        <div class="space-y-4 pt-4 border-t border-zinc-800">
                            <h3 class="font-bold text-lg">মন্তব্যসমূহ (${v.comments ? v.comments.length : 0})</h3>
                            <div class="flex space-x-3">
                                <img src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=100&h=100&fit=crop" class="w-10 h-10 rounded-full object-cover">
                                <div class="flex-1 space-y-2">
                                    <input type="text" id="newCommentInput" placeholder="একটি মন্তব্য যোগ করুন..." class="w-full bg-zinc-900 border border-zinc-700 rounded-xl px-4 py-2.5 text-sm text-zinc-100 focus:outline-none focus:border-red-500" onkeydown="if(event.key==='Enter') addComment('${v.id}')">
                                    <div class="flex justify-end">
                                        <button onclick="addComment('${v.id}')" class="bg-red-600 hover:bg-red-700 text-white px-5 py-1.5 rounded-xl text-xs font-semibold cursor-pointer">কমেন্ট করুন</button>
                                    </div>
                                </div>
                            </div>
                            <div class="space-y-3 pt-2" id="commentListContainer">
                                ${(!v.comments || v.comments.length === 0) ? '<p class="text-xs text-zinc-500">এখনো কোনো মন্তব্য করা হয়নি।</p>' : v.comments.map(c => `
                                    <div class="flex space-x-3 bg-zinc-900/40 border border-zinc-800/80 p-3 rounded-2xl">
                                        <img src="${c.avatar}" class="w-9 h-9 rounded-full object-cover">
                                        <div class="flex-1 text-sm">
                                            <div class="flex items-center space-x-2">
                                                <span class="font-semibold text-xs text-zinc-300">${c.user}</span>
                                                <span class="text-[10px] text-zinc-500">${c.time}</span>
                                            </div>
                                            <p class="text-zinc-200 mt-1">${c.text}</p>
                                        </div>
                                    </div>
                                `).join('')}
                            </div>
                        </div>
                    </div>

                    <!-- Related Videos Sidebar -->
                    <div class="space-y-3">
                        <h3 class="font-bold text-base text-zinc-200">সম্পর্কিত ভিডিওসমূহ</h3>
                        <div class="space-y-3">
                            ${videos.filter(x => x.id !== v.id).map(rel => `
                                <div class="flex space-x-3 cursor-pointer group" onclick="playVideo('${rel.id}')">
                                    <img src="${rel.thumbnail}" class="w-36 aspect-video rounded-xl object-cover bg-zinc-900 shrink-0">
                                    <div class="flex-1 overflow-hidden">
                                        <h4 class="font-semibold text-xs text-zinc-100 line-clamp-2 leading-snug group-hover:text-red-400 transition">${rel.title}</h4>
                                        <p class="text-[11px] text-zinc-400 mt-1">${rel.channel}</p>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                </div>
            `;
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function addComment(videoId) {
            const input = document.getElementById('newCommentInput');
            const text = input.value.trim();
            if (!text) return;
            const v = videos.find(x => x.id === videoId);
            if (!v) return;
            if (!v.comments) v.comments = [];
            v.comments.unshift({
                id: 'c_' + Date.now(),
                user: 'Fact Bangla',
                avatar: 'https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=100&h=100&fit=crop',
                text: text,
                time: 'এইমাত্র',
                likes: 0
            });
            if (db) {
                try {
                    const transaction = db.transaction(['videos'], 'readwrite');
                    transaction.objectStore('videos').put(v);
                } catch(err) { console.error(err); }
            }
            input.value = '';
            showToast('মন্তব্য সফলভাবে যোগ করা হয়েছে!');
            playVideo(videoId);
        }

        function toggleSubscribe(id) {
            const v = videos.find(x => x.id === id);
            if (!v) return;
            v.isSubscribed = !v.isSubscribed;
            updateSubscriptionsList();
            showToast(v.isSubscribed ? 'চ্যানেলটি সাবস্ক্রাইব করা হয়েছে!' : 'আনসাবস্ক্রাইব করা হয়েছে।');
            playVideo(id);
        }

        function toggleLike(id) {
            const v = videos.find(x => x.id === id);
            if (!v) return;
            const index = likedVideos.findIndex(item => item.id === id);
            if (index > -1) {
                likedVideos.splice(index, 1);
                showToast('লাইক সরানো হয়েছে।');
            } else {
                likedVideos.unshift(v);
                showToast('লাইক করা হয়েছে!');
            }
            saveUserDataToDB();
            playVideo(id);
        }

        function openStudio() {
            const main = document.getElementById('mainContent');
            main.innerHTML = `
                <div class="max-w-6xl mx-auto space-y-6">
                    <div class="flex items-center justify-between bg-cardbg border border-zinc-800 p-6 rounded-2xl shadow-lg">
                        <div>
                            <h1 class="text-2xl font-bold">ক্রিয়েটর স্টুডিও ড্যাশবোর্ড</h1>
                            <p class="text-sm text-zinc-400 mt-1">আপনার সকল ভিডিও এবং অ্যালগরিদম সেফটি স্ট্যাটাস ম্যানেজ করুন।</p>
                        </div>
                        <button onclick="openUploadModal()" class="bg-red-600 hover:bg-red-700 text-white px-5 py-2.5 rounded-xl font-medium text-sm transition shadow-lg cursor-pointer">নতুন ভিডিও আপলোড</button>
                    </div>
                    <div class="bg-cardbg border border-zinc-800 rounded-2xl overflow-hidden shadow-xl">
                        <div class="px-6 py-4 border-b border-zinc-800 font-bold text-base">আপলোডকৃত ভিডিও (${videos.length})</div>
                        <div class="divide-y divide-zinc-800" id="studioVideoList">
                            ${videos.map(v => `
                                <div class="flex items-center justify-between px-6 py-4">
                                    <div class="flex items-center space-x-4">
                                        <img src="${v.thumbnail}" class="w-24 ${v.videoType === 'short' ? 'short-card-aspect' : 'aspect-video'} rounded-xl object-cover bg-zinc-900">
                                        <div>
                                            <h4 class="font-bold text-sm text-zinc-100 line-clamp-1">${v.title}</h4>
                                            <p class="text-xs text-zinc-400 mt-0.5">ডিউরেশন: ${formatDuration(v.durationSeconds)} • ক্যাটাগরি: ${v.category} ${v.isAdult ? '• <span class="text-rose-400 font-bold">18+ Restricted</span>' : ''}</p>
                                        </div>
                                    </div>
                                    <button onclick="promptDeleteVideo('${v.id}')" class="bg-red-500/10 hover:bg-red-500/20 text-red-400 px-3 py-1.5 rounded-lg text-xs font-medium transition cursor-pointer">মুছে ফেলুন</button>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                </div>

                <div id="deleteConfirmModal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
                    <div class="bg-cardbg border border-zinc-700 w-full max-w-md rounded-2xl shadow-2xl p-6 space-y-4 text-center">
                        <div class="w-14 h-14 bg-red-600/20 text-red-500 rounded-full flex items-center justify-center mx-auto text-2xl">
                            <i class="fa-solid fa-triangle-exclamation"></i>
                        </div>
                        <h3 class="font-bold text-lg text-white">ভিডিও মুছে ফেলতে চান?</h3>
                        <p class="text-xs text-zinc-400" id="deleteModalSubText">নিশ্চিত করলে ভিডিওটি মুছে ফেলা হবে। ৫ সেকেন্ডের মধ্যে ক্যানসেল করতে পারবেন।</p>
                        
                        <div id="deleteCountdownBox" class="hidden py-2 px-4 bg-zinc-900 rounded-xl border border-zinc-800 font-bold text-red-500 text-sm">
                            মুছে ফেলা হচ্ছে... <span id="deleteCountdownTimer">5</span> সেকেন্ড বাকি
                        </div>

                        <div class="flex space-x-3 pt-2">
                            <button id="deleteBackBtn" onclick="cancelDeletePrompt()" class="flex-1 bg-zinc-800 hover:bg-zinc-700 text-zinc-200 py-2.5 rounded-xl text-sm font-medium transition cursor-pointer">ব্যাক (ফিরে যান)</button>
                            <button id="deleteConfirmBtn" onclick="startDeleteCountdown()" class="flex-1 bg-red-600 hover:bg-red-700 text-white py-2.5 rounded-xl text-sm font-medium transition shadow-lg cursor-pointer">কনফার্ম (মুছে ফেলুন)</button>
                        </div>
                    </div>
                </div>
            `;
        }

        let pendingDeleteVideoId = null;
        let deleteTimerInterval = null;

        function promptDeleteVideo(id) {
            pendingDeleteVideoId = id;
            document.getElementById('deleteConfirmModal').classList.remove('hidden');
            document.getElementById('deleteCountdownBox').classList.add('hidden');
            document.getElementById('deleteConfirmBtn').classList.remove('hidden');
            document.getElementById('deleteBackBtn').innerText = 'ব্যাক (ফিরে যান)';
            document.getElementById('deleteModalSubText').innerText = 'নিশ্চিত করলে ভিডিওটি মুছে ফেলা হবে। কনফার্ম করার পর ৫ সেকেন্ডের মধ্যে বাতিল করার সুযোগ থাকবে।';
        }

        function cancelDeletePrompt() {
            if (deleteTimerInterval) clearInterval(deleteTimerInterval);
            pendingDeleteVideoId = null;
            document.getElementById('deleteConfirmModal').classList.add('hidden');
        }

        function startDeleteCountdown() {
            document.getElementById('deleteConfirmBtn').classList.add('hidden');
            const countdownBox = document.getElementById('deleteCountdownBox');
            countdownBox.classList.remove('hidden');
            document.getElementById('deleteBackBtn').innerText = 'ক্যানসেল (বাতিল করুন)';
            document.getElementById('deleteModalSubText').innerText = 'ভিডিওটি মুছে ফেলা হতে চলেছে। চাইলে এখনই ক্যানসেল করুন।';

            let timeLeft = 5;
            document.getElementById('deleteCountdownTimer').innerText = timeLeft;

            deleteTimerInterval = setInterval(() => {
                timeLeft--;
                document.getElementById('deleteCountdownTimer').innerText = timeLeft;
                if (timeLeft <= 0) {
                    clearInterval(deleteTimerInterval);
                    executeDeleteVideo(pendingDeleteVideoId);
                }
            }, 1000);
        }

        function executeDeleteVideo(id) {
            cancelDeletePrompt();
            videos = videos.filter(v => v.id !== id);
            if (db) {
                try {
                    const transaction = db.transaction(['videos'], 'readwrite');
                    transaction.objectStore('videos').delete(id);
                } catch(err) { console.error(err); }
            }
            updateSubscriptionsList();
            openStudio();
            showToast('ভিডিও সফলভাবে মুছে ফেলা হয়েছে।');
        }

        function publishVideo() {
            const title = document.getElementById('uploadTitle').value.trim();
            const channel = document.getElementById('uploadChannel').value.trim() || 'প্রফেশনাল ক্রিয়েটর';
            const category = document.getElementById('uploadCategory').value;
            const desc = document.getElementById('uploadDesc').value.trim();
            const thumb = document.getElementById('uploadThumb').value.trim();

            if (!title) {
                showToast('দয়া করে শিরোনাম দিন।', 'error');
                return;
            }

            const isAdultContent = window.tempDetected18Plus || false;
            const uploadTimeNow = Date.now();
            const formattedTimeStr = new Date(uploadTimeNow).toLocaleString('bn-BD', {dateStyle: 'medium', timeStyle: 'short'});

            const newVideo = {
                id: 'v_' + uploadTimeNow,
                title: title,
                channel: channel,
                avatar: 'https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=100&h=100&fit=crop',
                views: '১ ভিউ',
                time: formattedTimeStr,
                uploadTimestamp: uploadTimeNow,
                thumbnail: thumb || (currentUploadType === 'short' ? 'https://images.unsplash.com/photo-1517694712202-14dd9538aa97?w=400&h=700&fit=crop' : 'https://images.unsplash.com/photo-1555066931-4365d14bab8c?w=600&h=350&fit=crop'),
                videoBlob: selectedFileBlob,
                description: desc || 'বর্ণনা নেই।',
                likes: '০',
                category: category,
                videoType: currentUploadType,
                isAdult: isAdultContent,
                durationSeconds: selectedFileDuration || 120,
                isSubscribed: false,
                comments: []
            };

            videos.unshift(newVideo);
            if (db) {
                try {
                    const transaction = db.transaction(['videos'], 'readwrite');
                    transaction.objectStore('videos').put(newVideo);
                } catch(err) { console.error(err); }
            }

            closeUploadModal();
            switchTab('home');
            showToast('ভিডিও সফলভাবে প্রকাশিত হয়েছে!');
        }

        function handleSearchModalInput() {
            const query = document.getElementById('searchInput').value.trim();
            if (!query) return;
            toggleSearchModal();
            renderSearchResults(query);
        }

        function quickSearchTag(tag) {
            toggleSearchModal();
            renderSearchResults(tag);
        }

        function renderSearchResults(query) {
            const queryLower = query.toLowerCase();
            const filtered = videos.filter(v => v.title.toLowerCase().includes(queryLower) || v.category.toLowerCase().includes(queryLower) || v.channel.toLowerCase().includes(queryLower));
            const main = document.getElementById('mainContent');
            main.innerHTML = `
                <div class="max-w-5xl mx-auto space-y-4">
                    <h2 class="text-xl font-bold">"${query}" এর অনুসন্ধান ফলাফল (${filtered.length})</h2>
                    ${filtered.length === 0 ? `
                        <div class="text-center py-16 bg-cardbg border border-zinc-800 rounded-2xl">
                            <i class="fa-solid fa-magnifying-glass text-4xl text-zinc-600 mb-3"></i>
                            <h3 class="font-bold text-lg">কোনো ভিডিও পাওয়া যায়নি</h3>
                        </div>
                    ` : `
                        <div class="space-y-3">
                            ${filtered.map(v => `
                                <div class="flex gap-4 bg-cardbg border border-zinc-800 p-4 rounded-2xl cursor-pointer hover:border-zinc-700 transition" onclick="playVideo('${v.id}')">
                                    <img src="${v.thumbnail}" class="w-48 aspect-video rounded-xl object-cover bg-zinc-900">
                                    <div class="flex-1">
                                        <h3 class="font-bold text-sm text-zinc-100">${v.title}</h3>
                                        <p class="text-xs text-zinc-400 mt-1">${v.channel} • ডিউরেশন: ${formatDuration(v.durationSeconds)}</p>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                    `}
                </div>
            `;
        }

        function showToast(msg, type = 'success') {
            const toast = document.getElementById('toast');
            const toastMsg = document.getElementById('toastMsg');
            const toastIcon = document.getElementById('toastIcon');
            toastMsg.innerText = msg;
            toastIcon.className = type === 'success' ? 'fa-solid fa-circle-check text-emerald-400 text-lg' : 'fa-solid fa-triangle-exclamation text-red-400 text-lg';
            toast.classList.remove('translate-y-32', 'opacity-0');
            setTimeout(() => toast.classList.add('translate-y-32', 'opacity-0'), 3000);
        }
    </script>
</body>
</html>
