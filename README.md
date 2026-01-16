# hiro.list.co
Top 50 Openings list
import React, { useEffect, useMemo, useState } from "react";
import { motion } from "framer-motion";

const initialOpenings = [
  { id: 1, anime: "Death Note", title: "Alumina (ED1)", artist: "THE NIGHTMARE", url: "https://v.animethemes.moe/DeathNote-ED1.webm" },
  { id: 2, anime: "To Love Ru", title: "forever we can make it! (OP1)", artist: "THYME", url: "https://v.animethemes.moe/ToLoveRu-OP1.webm" },
  { id: 3, anime: "Parasyte -the maxim-", title: "Let Me Hear", artist: "Fear, and Loathing in Las Vegas", url: "https://v.animethemes.moe/Kiseijuu-OP1.webm" },
  { id: 4, anime: "Tokyo Ghoul √A", title: "Munou (OP1)", artist: "österreich", url: "https://v.animethemes.moe/TokyoGhoulRootA-OP1.webm" },
  { id: 5, anime: "Toaru Majutsu no Index", title: "Masterpiece (OP2)", artist: "Kawada Mami", url: "https://v.animethemes.moe/ToaruMajutsuNoIndex-OP2.webm" },
  { id: 6, anime: "Black Bullet", title: "Tokohana (ED1)", artist: "Mimori Suzuko", url: "https://v.animethemes.moe/BlackBullet-ED1.webm" },
  { id: 7, anime: "Giji Harem", title: "OP1", artist: "VA Cast", url: "https://v.animethemes.moe/GijiHarem-OP1.webm" },
  { id: 8, anime: "Monogatari Series: Second Season", title: "Mousou Express (OP3)", artist: "Yuka Iguchi", url: "https://v.animethemes.moe/MonogatariSS-OP3.webm" },
  { id: 9, anime: "Monogatari Series: Second Season", title: "White Lies (OP4)", artist: "Kana Hanazawa", url: "https://v.animethemes.moe/MonogatariSS-OP4-BD.webm" },
  { id: 10, anime: "Nisekoi", title: "Step (OP2)", artist: "ClariS", url: "https://v.animethemes.moe/Nisekoi-OP2.webm" },
  { id: 11, anime: "Bleach", title: "Asterisk (OP1)", artist: "ORANGE RANGE", url: "https://v.animethemes.moe/Bleach-OP1.webm" },
  { id: 12, anime: "Bleach", title: "Alones (OP6)", artist: "Aqua Timez", url: "https://v.animethemes.moe/Bleach-OP6.webm" },
  { id: 13, anime: "Toradora!", title: "Vanilla Salt (ED1)", artist: "Yui Horie", url: "https://v.animethemes.moe/Toradora-ED1.webm" },
  { id: 14, anime: "Sayonara Zetsubou Sensei", title: "Zetsubou Billy (OP1)", artist: "MAXIMUM THE HORMONE", url: "https://v.animethemes.moe/ZanSayonaraZetsubouSensei-OP1.webm" },
  { id: 15, anime: "Mirai Nikki Redial", title: "Redial (OP1)", artist: "Yousei Teikoku", url: "https://v.animethemes.moe/MiraiNikkiRedial-OP1.webm" },
  { id: 16, anime: "Hunter x Hunter (2011)", title: "Just Awake (ED1)", artist: "Fear, and Loathing in Las Vegas", url: "https://v.animethemes.moe/HunterHunter2011-ED1.webm" },
  { id: 17, anime: "No Game No Life", title: "Oracion (ED1)", artist: "Yuka Iguchi", url: "https://v.animethemes.moe/NoGameNoLife-ED1.webm" },
  { id: 18, anime: "Asobi Asobase", title: "Asobi Asobase (OP1)", artist: "VA Cast", url: "https://v.animethemes.moe/AsobiAsobase-OP1-NCBD1080.webm" },
  { id: 19, anime: "Denpa Onna to Seishun Otoko", title: "Os-Uchuujin (OP1)", artist: "Shintani Ryoko", url: "https://v.animethemes.moe/DenpaOnnaToSeishunOtoko-OP1.webm" },
  { id: 20, anime: "Black Clover", title: "Paint it Black (OP2)", artist: "BISH", url: "https://v.animethemes.moe/BlackClover-OP2v4-NCBD1080.webm" },
  { id: 21, anime: "Black Clover", title: "Gamushara (OP5)", artist: "Miyuna", url: "https://v.animethemes.moe/BlackClover-OP5-NCBD1080.webm" },
  { id: 22, anime: "Durarara!!", title: "Complication (OP2)", artist: "ROOKiEZ is PUNK'D", url: "https://v.animethemes.moe/Durarara-OP2.webm" },
  { id: 23, anime: "Captain Tsubasa: Road to 2002 (Oliver e Benji 2002)", title: "Anjo Alado (ED – Portuguese)", artist: "NIGHTMARE", url: "https://youtu.be/KzP1MntXTF0", isYouTube: true },
  { id: 24, anime: "Kyouran Kazoku Nikki", title: "Kyouran Senki ~Nichijou no Kami-sama~ (ED1)", artist: "Ayumi Fujimura", url: "https://youtu.be/fFtSTOcQ018", isYouTube: true },
  { id: 25, anime: "Golden Time", title: "The♡World's♡End (OP2)", artist: "Yui Horie", url: "https://v.animethemes.moe/GoldenTime-OP2.webm" },
  { id: 26, anime: "Girls' Last Tour", title: "More One Night (ED1)", artist: "Inori Minase", url: "https://v.animethemes.moe/ShoujoShuumatsuRyokou-ED1-NCBD1080.webm" },
  { id: 27, anime: "Chobits", title: "Let Me Be With You (OP1)", artist: "ROUND TABLE", url: "https://v.animethemes.moe/Chobits-OP1.webm" },
  { id: 28, anime: "NHK ni Youkoso!", title: "Puzzle (OP1)", artist: "ROUND TABLE", url: "https://v.animethemes.moe/NHKNiYoukoso-OP1.webm" },
  { id: 29, anime: "Dororo", title: "Kaen (OP1)", artist: "Queen Bee", url: "https://v.animethemes.moe/Dororo2019-OP1-NCBD1080.webm" },
  { id: 30, anime: "Psycho-Pass", title: "Namae no Nai Kaibutsu (ED1)", artist: "EGOIST", url: "https://v.animethemes.moe/PsychoPass-ED1.webm" },
  { id: 31, anime: "Guilty Crown", title: "The Everlasting Guilty Crown (OP3)", artist: "EGOIST", url: "https://v.animethemes.moe/GuiltyCrown-OP3.webm" },
  { id: 32, anime: "Naruto Shippuden", title: "Silhouette (OP7)", artist: "KANA-BOON", url: "https://v.animethemes.moe/NarutoShippuuden-OP7.webm" },
  { id: 33, anime: "Fullmetal Alchemist: Brotherhood", title: "Again (OP1)", artist: "YUI", url: "https://v.animethemes.moe/FullmetalAlchemistBrotherhood-OP1.webm" },
  { id: 34, anime: "One Piece", title: "One Day (OP13)", artist: "The ROOTLESS", url: "https://v.animethemes.moe/OnePiece-OP13-NCBD.webm" },
  { id: 35, anime: "Soul Eater", title: "Papermoon (OP2)", artist: "Tommy heavenly6", url: "https://v.animethemes.moe/SoulEater-OP2.webm" },
  { id: 36, anime: "Gintama", title: "Pray (OP1)", artist: "Tommy heavenly6", url: "https://v.animethemes.moe/Gintama-OP1.webm" },
  { id: 37, anime: "Gintama Enchousen", title: "Sakura Mitsutsuki (OP3)", artist: "SPYAIR", url: "https://v.animethemes.moe/GintamaEnchousen-OP3-NCBD1080.webm" },
  { id: 38, anime: "Texhnolyze", title: "Guardian Angel (OP1)", artist: "Juno Reactor", url: "https://v.animethemes.moe/Texhnolyze-OP1.webm" },
  { id: 39, anime: "Gantz", title: "Super Shooter (OP1)", artist: "RIP SLYME", url: "https://v.animethemes.moe/Gantz-OP1.webm" },
  { id: 40, anime: "Ergo Proxy", title: "Kiri (OP1)", artist: "MONORAL", url: "https://v.animethemes.moe/ErgoProxy-OP1.webm" },
  { id: 41, anime: "Elfen Lied", title: "Lilium (OP1)", artist: "Kumiko Noma", url: "https://v.animethemes.moe/ElfenLied-OP1.webm" },
  { id: 42, anime: "AIR", title: "Tori no Uta (OP1)", artist: "Lia", url: "https://v.animethemes.moe/Air-OP1.webm" },
  { id: 43, anime: "Clannad After Story", title: "Toki wo Kizamu Uta (OP1)", artist: "Lia", url: "https://v.animethemes.moe/ClannadAfterStory-OP1.webm" },
  { id: 44, anime: "The World God Only Knows", title: "God only knows (OP1)", artist: "Oratorio The World God Only Knows", url: "https://v.animethemes.moe/Kaminomi-OP1-NCBD1080.webm" },
  { id: 45, anime: "Magic Kaito 1412", title: "Kimi no Matsu Sekai (OP2)", artist: "L'Arc~en~Ciel", url: "https://v.animethemes.moe/MagicKaito1412-OP2.webm" },
  { id: 46, anime: "Higurashi no Naku Koro ni", title: "Higurashi no Naku Koro ni (OP1)", artist: "Eiko Shimamiya", url: "https://v.animethemes.moe/Higurashi-OP1.webm" },
  { id: 47, anime: "Steins;Gate", title: "Hacking to the Gate (OP1)", artist: "Kanako Itou", url: "https://v.animethemes.moe/SteinsGate-OP1.webm" },
  { id: 48, anime: "Great Teacher Onizuka", title: "Driver's High (OP2)", artist: "L'Arc~en~Ciel", url: "https://v.animethemes.moe/GreatTeacherOnizuka-OP2.webm" },
  { id: 49, anime: "Pop Team Epic", title: "POP TEAM EPIC (OP2)", artist: "Sumire Uesaka", url: "https://v.animethemes.moe/PopTeamEpic-OP2-NCBD1080.webm" },
  { id: 50, anime: "Erased", title: "Re:Re: (OP1)", artist: "Asian Kung-Fu Generation", url: "https://v.animethemes.moe/BokuDakeGaInaiMachi-OP1.webm" }
];

export default function App() {
  const [ratings, setRatings] = useState(() => {
    const urlParams = new URLSearchParams(window.location.search);
    const shared = urlParams.get('scores');
    if (shared) {
      try {
        return JSON.parse(atob(shared));
      } catch {
        return JSON.parse(localStorage.getItem('ratings') || '{}');
      }
    }
    return JSON.parse(localStorage.getItem('ratings') || '{}');
  });

  const [globalRatings, setGlobalRatings] = useState(() => JSON.parse(localStorage.getItem('globalRatings') || '{}'));
  const [notes, setNotes] = useState(() => JSON.parse(localStorage.getItem('notes') || '{}'));
  const [sortBy, setSortBy] = useState("rank");

  useEffect(() => {
    localStorage.setItem('ratings', JSON.stringify(ratings));
    localStorage.setItem('notes', JSON.stringify(notes));
  }, [ratings, notes]);

  const avg = (id) => {
    const scores = globalRatings[id] || [];
    if (!scores.length) return null;
    return (scores.reduce((a, b) => a + b, 0) / scores.length).toFixed(1);
  };

  const sorted = useMemo(() => {
    const list = [...initialOpenings];
    if (sortBy === "rating") list.sort((a, b) => (avg(b.id) || 0) - (avg(a.id) || 0));
    return list;
  }, [ratings, sortBy, globalRatings]);

  const podium = sorted.filter(o => avg(o.id)).slice(0, 3);

  return (
    <div className="min-h-screen bg-gradient-to-br from-purple-900 via-black to-indigo-900 text-white px-3 sm:px-6 py-6">
      <h1 className="text-3xl sm:text-4xl font-bold text-center mb-8">🏆 Anime OP / ED Top 50 🏆</h1>

      <div className="flex flex-col sm:flex-row justify-center gap-4 mb-10">
        {podium.map((p, i) => (
          <motion.div key={p.id} initial={{ opacity: 0, y: 30 }} animate={{ opacity: 1, y: 0 }} transition={{ delay: i * 0.15, type: "spring" }} className="bg-yellow-500/20 border border-yellow-400 rounded-2xl p-4 text-center">
            <div className="text-xl font-bold">#{i + 1}</div>
            <div className="font-semibold">{p.anime}</div>
            <div className="text-sm opacity-80">{p.title}</div>
            <div className="text-2xl mt-2">⭐ {avg(p.id)}</div>
          </motion.div>
        ))}
      </div>

      <div className="flex justify-center mb-6">
        <select value={sortBy} onChange={(e) => setSortBy(e.target.value)} className="bg-purple-800 p-2 rounded">
          <option value="rank">Sort by Rank</option>
          <option value="rating">Sort by Rating</option>
        </select>
      </div>

      <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
        {sorted.map((op, index) => (
          <motion.div key={op.id} layout className="bg-black/60 border border-purple-500 rounded-2xl p-3 sm:p-4">
            <h2 className="font-bold text-sm sm:text-base">#{index + 1} {op.anime}</h2>
            <p className="text-xs sm:text-sm text-purple-300">{op.title} {op.artist && `– ${op.artist}`}</p>
            {op.isYouTube ? (
              <iframe className="w-full aspect-video" src={op.url} frameBorder="0" allowFullScreen title={`${op.anime} video`} />
            ) : (
              <video className="w-full aspect-video rounded" src={op.url} controls />
