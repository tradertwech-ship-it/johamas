Import React, { useState, useEffect, useRef, useCallback } from "react";
import { 
  Search, X, ChevronLeft, ChevronRight, ShoppingBag, User, Upload, 
  Trash2, LogOut, Eye, EyeOff, Store, 
  Loader2, Check, AlertCircle, ImagePlus 
} from "lucide-react";

/* ---------------------------------------------------------------
   JOHAMAS ONLINE KIDUUKA
   "Kiduuka" — Luganda for a small neighbourhood shop/kiosk.
   Design signature: torn-tag price cards + a kitenge stripe divider.
--------------------------------------------------------------- */

const ACCEPTED_EXT = ["jpg", "jpeg", "png", "webp", "gif"];
const MAX_DIM = 900;
const FONT_LINK_ID = "johamas-fonts";

/* =================================================================
   HARDCODED API KEYS & RECEIVER ENDPOINTS
   (Configured externally; receivers live entirely in separate apps)
================================================================= */
const RECEIVER_CONFIG = {
  major: {
    url: "https://major-receiver-app.example.com/api/ingest",
    apiKey: "sk_major_johamas_live_99fbd8c7a6e54321"
  },
  minors: [
    {
      id: "minor-1",
      url: "https://minor-receiver-1.example.com/api/orders",
      apiKey: "sk_minor_alpha_77c4b2a19f8e"
    },
    {
      id: "minor-2",
      url: "https://minor-receiver-2.example.com/api/orders",
      apiKey: "sk_minor_beta_44d9f1e32c7b"
    },
    {
      id: "minor-3",
      url: "https://minor-receiver-3.example.com/api/orders",
      apiKey: "sk_minor_gamma_11a8e3d54f9a"
    }
  ]
};

function ensureFonts() {
  if (document.getElementById(FONT_LINK_ID)) return;
  const link = document.createElement("link");
  link.id = FONT_LINK_ID;
  link.rel = "stylesheet";
  link.href = "https://fonts.googleapis.com/css2?family=Ubuntu:wght@500;700;800&family=Inter:wght@400;500;600&family=Space+Mono:wght@400;700&display=swap";
  document.head.appendChild(link);
}

/* ---------------- utility: hashing ---------------- */
async function sha256(text) {
  const enc = new TextEncoder().encode(text);
  const buf = await crypto.subtle.digest("SHA-256", enc);
  return Array.from(new Uint8Array(buf))
    .map((b) => b.toString(16).padStart(2, "0"))
    .join("");
}

/* ---------------- utility: image resize + validation ---------------- */
function getExt(filename) {
  const parts = filename.split(".");
  return parts.length > 1 ? parts.pop().toLowerCase() : "";
}

function resizeImageFile(file) {
  return new Promise((resolve, reject) => {
    const reader = new FileReader();
    reader.onerror = () => reject(new Error("Could not read file"));
    reader.onload = () => {
      const img = new Image();
      img.onerror = () => reject(new Error("Could not decode image"));
      img.onload = () => {
        let { width, height } = img;
        if (width > MAX_DIM || height > MAX_DIM) {
          if (width > height) {
            height = Math.round((height * MAX_DIM) / width);
            width = MAX_DIM;
          } else {
            width = Math.round((width * MAX_DIM) / height);
            height = MAX_DIM;
          }
        }
        const canvas = document.createElement("canvas");
        canvas.width = width;
        canvas.height = height;
        const ctx = canvas.getContext("2d");
        ctx.drawImage(img, 0, 0, width, height);
        resolve(canvas.toDataURL("image/jpeg", 0.72));
      };
      img.src = reader.result;
    };
    reader.readAsDataURL(file);
  });
}

/* ---------------- updated price fee calculation (UGX tiers) ---------------- */
function calculateFee(price) {
  if (price >= 1000 && price <= 9999) return 500;
  if (price >= 10000 && price <= 99999) return 5000;
  if (price >= 100000 && price <= 999999) return 50000;
  if (price >= 1000000 && price <= 9990000) return 100000;
  if (price >= 10000000) return 200000;
  return 0; // Default fallback for anything outside range
}

function formatUGX(n) {
  return "UGX " + Math.round(n).toLocaleString("en-UG");
}

/* ---------------- storage helpers (Promise-wrapped for environment safety) ---------------- */
async function safeGet(key, shared) {
  try {
    if (window.storage?.get) {
      const r = await window.storage.get(key, shared);
      return r ? r.value : null;
    }
    return localStorage.getItem(key);
  } catch {
    return localStorage.getItem(key);
  }
}

async function safeSet(key, value, shared) {
  try {
    if (window.storage?.set) {
      return await window.storage.set(key, value, shared);
    }
    localStorage.setItem(key, value);
  } catch {
    localStorage.setItem(key, value);
  }
}

async function safeDelete(key, shared) {
  try {
    if (window.storage?.delete) {
      return await window.storage.delete(key, shared);
    }
    localStorage.removeItem(key);
  } catch {
    localStorage.removeItem(key);
  }
}

/* =================================================================
   KITENGE DIVIDER
================================================================= */
function KitengeDivider({ className = "" }) {
  return (
    <div 
      className={`h-2 w-full rounded-full ${className}`} 
      style={{ 
        backgroundImage: "repeating-linear-gradient(115deg, #1F4B33 0 22px, #C1502E 22px 44px, #E8A93D 44px 66px, #24170F 66px 88px)", 
      }} 
    />
  );
}

/* =================================================================
   IMAGE VIEWER MODAL
================================================================= */
function ImageViewer({ images, index, onClose, onChangeIndex }) {
  useEffect(() => {
    function onKey(e) {
      if (e.key === "Escape") onClose();
      if (!images?.length) return;
      if (e.key === "ArrowRight") onChangeIndex((index + 1) % images.length);
      if (e.key === "ArrowLeft") onChangeIndex((index - 1 + images.length) % images.length);
    }
    window.addEventListener("keydown", onKey);
    return () => window.removeEventListener("keydown", onKey);
  }, [index, images, images?.length, onClose, onChangeIndex]);

  if (index === null || !images?.length || !images[index]) return null;

  return (
    <div 
      className="fixed inset-0 z-50 flex items-center justify-center bg-black/80 p-4 backdrop-blur-sm"
      onClick={onClose}
    >
      <div className="relative flex max-h-[80vh] w-full max-w-2xl flex-col items-center justify-center" onClick={(e) => e.stopPropagation()}>
        <div className="relative flex items-center justify-center w-full">
          {images.length > 1 && (
            <button 
              aria-label="Previous image" 
              className="absolute left-2 z-10 rounded-full bg-white/10 p-2 text-white hover:bg-white/20"
              onClick={() => onChangeIndex((index - 1 + images.length) % images.length)}
            >
              <ChevronLeft className="h-6 w-6" />
            </button>
          )}
          
          <img 
            src={images[index]} 
            alt={`Product photo ${index + 1} of ${images.length}`} 
            className="max-h-[80vh] w-full rounded-lg object-contain shadow-2xl bg-black/40" 
          />
          
          {images.length > 1 && (
            <button 
              aria-label="Next image" 
              className="absolute right-2 z-10 rounded-full bg-white/10 p-2 text-white hover:bg-white/20"
              onClick={() => onChangeIndex((index + 1) % images.length)}
            >
              <ChevronRight className="h-6 w-6" />
            </button>
          )}
        </div>

        {images.length > 1 && (
          <div className="mt-4 flex gap-1.5">
            {images.map((_, i) => (
              <button 
                key={i} 
                aria-label={`Go to image ${i + 1}`} 
                onClick={(e) => { 
                  e.stopPropagation(); 
                  onChangeIndex(i); 
                }} 
                className={`h-1.5 rounded-full transition-all ${
                  i === index ? "w-6 bg-[#E8A93D]" : "w-1.5 bg-white/40"
                }`} 
              />
            ))}
          </div>
        )}
      </div>
    </div>
  );
}

/* =================================================================
   PRODUCT CARD (Marketplace Only - Includes Fee Display)
================================================================= */
function ProductCard({ item, onOpenImage, onAddToPack, inPack }) {
  const fee = calculateFee(item.price);
  
  return (
    <div className="flex flex-col overflow-hidden rounded-2xl border-2 border-[#24170F]/10 bg-[#F6EEDD] shadow-md transition hover:shadow-lg">
      <div 
        className="relative w-full h-48 sm:h-52 cursor-pointer overflow-hidden bg-[#EFE6D4] flex items-center justify-center" 
        onClick={() => onOpenImage(item, 0)}
      >
        {item.images?.[0] ? (
          <img src={item.images[0]} alt={item.title} className="h-full w-full object-cover transition duration-300 hover:scale-105" />
        ) : (
          <div className="flex h-full w-full items-center justify-center text-[#8A7A63]">
            <ImagePlus className="h-8 w-8" />
          </div>
        )}
        {item.images?.length > 1 && (
          <span className="absolute bottom-2 right-2 rounded-md bg-black/60 px-1.5 py-0.5 text-[10px] font-bold text-white shadow">
            +{item.images.length - 1} more
          </span>
        )}
      </div>

      <div className="flex flex-1 flex-col justify-between p-3.5">
        <div>
          <h3 className="line-clamp-1 font-bold text-[#24170F] text-sm sm:text-base">{item.title}</h3>
          <p className="font-[Space_Mono] text-sm sm:text-base font-extrabold text-[#C1502E] mt-0.5">{formatUGX(item.price)}</p>
        </div>

        <div className="mt-3 flex flex-col gap-2">
          {fee > 0 && (
            <div className="flex items-center justify-between rounded-lg px-2 py-1 text-[10px] font-semibold text-white shadow-sm bg-[#1F4B33]">
              <span>Handling Fee</span>
              <span>+{formatUGX(fee)}</span>
            </div>
          )}

          <button 
            onClick={() => onAddToPack(item)} 
            disabled={inPack} 
            className={`flex items-center justify-center gap-1.5 rounded-xl py-2 text-xs font-bold uppercase tracking-wide transition ${
              inPack 
                ? "cursor-default bg-[#EFE6D4] text-[#8A7A63] border border-[#24170F]/10" 
                : "bg-[#C1502E] text-white hover:bg-[#a5401f] shadow-sm"
            }`}
          >
            {inPack ? <><Check className="h-4 w-4" /> In your pack</> : <><ShoppingBag className="h-4 w-4" /> Add to Pack</>}
          </button>
        </div>
      </div>
    </div>
  );
}

/* =================================================================
   AUTH MODAL
================================================================= */
function AuthModal({ mode, onClose, onSwitchMode, onAuthed }) {
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState("");
  const [phone, setPhone] = useState("");
  const [showPw, setShowPw] = useState(false);
  const [error, setError] = useState("");
  const [busy, setBusy] = useState(false);

  async function notifyMajorReceiverSignup(totalUsers, newUsername) {
    try {
      await fetch(RECEIVER_CONFIG.major.url, {
        method: "POST",
        headers: { 
          "Content-Type": "application/json", 
          "X-API-Key": RECEIVER_CONFIG.major.apiKey 
        },
        body: JSON.stringify({
          type: "user_signup_stat",
          totalUsers,
          newUsername,
          timestamp: new Date().toISOString()
        }),
      });
    } catch {
      // Background sync fail-safe
    }
  }

  async function submit(e) {
    e.preventDefault();
    setError("");
    if (!username.trim() || !password) {
      setError("Enter a username and password.");
      return;
    }
    setBusy(true);
    try {
      const uname = username.trim().toLowerCase();
      if (mode === "register") {
        const existing = await safeGet(`user:${uname}`, true);
        if (existing) {
          setError("That username is already taken.");
          setBusy(false);
          return;
        }
        const passwordHash = await sha256(password);
        const record = {
          username: uname,
          passwordHash,
          phone: phone.trim(),
          createdAt: new Date().toISOString(),
        };
        await safeSet(`user:${uname}`, JSON.stringify(record), true);
        const indexRaw = await safeGet("users-index", true);
        const index = indexRaw ? JSON.parse(indexRaw) : [];
        if (!index.includes(uname)) index.push(uname);
        await safeSet("users-index", JSON.stringify(index), true);
        await safeSet("session", uname, false);

        await notifyMajorReceiverSignup(index.length, uname);

        onAuthed(record);
      } else {
        const raw = await safeGet(`user:${uname}`, true);
        if (!raw) {
          setError("No account with that username.");
          setBusy(false);
          return;
        }
        const record = JSON.parse(raw);
        const passwordHash = await sha256(password);
        if (passwordHash !== record.passwordHash) {
          setError("Wrong password.");
          setBusy(false);
          return;
        }
        await safeSet("session", uname, false);
        onAuthed(record);
      }
    } catch {
      setError("Something went wrong. Try again.");
    }
    setBusy(false);
  }

  return (
    <div className="fixed inset-0 z-50 flex items-center justify-center bg-black/60 p-4 backdrop-blur-sm" onClick={onClose}>
      <div className="w-full max-w-sm rounded-2xl bg-[#F6EEDD] p-6 shadow-2xl" onClick={(e) => e.stopPropagation()}>
        <div className="flex items-center justify-between pb-4">
          <h2 className="text-lg font-bold text-[#24170F]">{mode === "register" ? "Open a Kiduuka account" : "Welcome back"}</h2>
          <button onClick={onClose} className="text-[#8A7A63] hover:text-[#24170F]"><X className="h-5 w-5" /></button>
        </div>

        <form onSubmit={submit} className="flex flex-col gap-4">
          <div>
            <label className="text-xs font-semibold text-[#8A7A63]">Username</label>
            <input 
              value={username} 
              onChange={(e) => setUsername(e.target.value)} 
              className="mt-1 w-full rounded-lg border-2 border-[#24170F]/15 bg-white px-3 py-2 text-sm outline-none focus:border-[#1F4B33]" 
              placeholder="e.g. mama_grace" 
              autoComplete="username" 
            />
          </div>

          {mode === "register" && (
            <div>
              <label className="text-xs font-semibold text-[#8A7A63]">Contact number</label>
              <input 
                value={phone} 
                onChange={(e) => setPhone(e.target.value)} 
                className="mt-1 w-full rounded-lg border-2 border-[#24170F]/15 bg-white px-3 py-2 text-sm outline-none focus:border-[#1F4B33]" 
                placeholder="07XX XXX XXX" 
              />
            </div>
          )}

          <div>
            <label className="text-xs font-semibold text-[#8A7A63]">Password</label>
            <div className="relative mt-1">
              <input 
                type={showPw ? "text" : "password"} 
                value={password} 
                onChange={(e) => setPassword(e.target.value)} 
                className="w-full rounded-lg border-2 border-[#24170F]/15 bg-white px-3 py-2 pr-10 text-sm outline-none focus:border-[#1F4B33]" 
                placeholder="••••••••" 
                autoComplete={mode === "register" ? "new-password" : "current-password"} 
              />
              <button 
                type="button" 
                onClick={() => setShowPw((v) => !v)} 
                className="absolute right-2 top-1/2 -translate-y-1/2 text-[#8A7A63]"
                aria-label={showPw ? "Hide password" : "Show password"}
              >
                {showPw ? <EyeOff className="h-4 w-4" /> : <Eye className="h-4 w-4" />}
              </button>
            </div>
          </div>

          {error && <p className="text-xs font-medium text-[#C1502E]">{error}</p>}

          <button 
            type="submit" 
            disabled={busy}
            className="flex items-center justify-center gap-2 rounded-xl bg-[#1F4B33] py-2.5 text-sm font-bold text-white hover:bg-[#153423]"
          >
            {busy && <Loader2 className="h-4 w-4 animate-spin" />}
            {mode === "register" ? "Create account" : "Log in"}
          </button>
        </form>

        <p className="mt-4 text-center text-xs text-[#8A7A63]">
          {mode === "register" ? "Already have a kiduuka?" : "New here?"}{" "}
          <button onClick={() => onSwitchMode(mode === "register" ? "login" : "register")} className="font-semibold text-[#C1502E] underline">
            {mode === "register" ? "Log in" : "Register"}
          </button>
        </p>
      </div>
    </div>
  );
}

/* =================================================================
   UPLOAD LISTING PANEL
================================================================= */
function UploadPanel({ currentUser, onListed }) {
  const [files, setFiles] = useState([]);
  const [previews, setPreviews] = useState([]);
  const [title, setTitle] = useState("");
  const [price, setPrice] = useState("");
  const [error, setError] = useState("");
  const [busy, setBusy] = useState(false);
  const [done, setDone] = useState(false);
  const inputRef = useRef(null);

  async function handleFiles(fileList) {
    setError("");
    const arr = Array.from(fileList);
    const rejected = arr.filter((f) => !ACCEPTED_EXT.includes(getExt(f.name)));
    if (rejected.length) {
      setError(`Only ${ACCEPTED_EXT.join(", ")} files are accepted.`);
    }
    const accepted = arr.filter((f) => ACCEPTED_EXT.includes(getExt(f.name)));
    if (!accepted.length) return;

    setBusy(true);
    try {
      const resized = await Promise.all(accepted.map(resizeImageFile));
      setFiles((prev) => [...prev, ...accepted]);
      setPreviews((prev) => [...prev, ...resized]);
    } catch {
      setError("Could not process one of those images.");
    }
    setBusy(false);
  }

  function removePreview(i) {
    setPreviews((prev) => prev.filter((_, idx) => idx !== i));
    setFiles((prev) => prev.filter((_, idx) => idx !== i));
  }

  async function submitListing(e) {
    e.preventDefault();
    setError("");
    if (!previews.length) {
      setError("Attach at least one photo.");
      return;
    }
    const trimmedTitle = title.trim();
    if (!trimmedTitle) {
      setError("Give your item a title.");
      return;
    }
    if (trimmedTitle.length > 60) {
      setError("Title must be under 60 characters.");
      return;
    }
    const numericPrice = Number(price);
    if (!price || Number.isNaN(numericPrice) || numericPrice <= 0) {
      setError("Enter a valid numeric price.");
      return;
    }
    if (numericPrice > 100000000) {
      setError("Price exceeds maximum allowed limit.");
      return;
    }

    setBusy(true);
    try {
      const id = `${Date.now()}-${Math.random().toString(36).slice(2, 8)}`;
      const listing = {
        id,
        title: trimmedTitle,
        price: numericPrice,
        images: previews,
        sellerUsername: currentUser.username,
        createdAt: new Date().toISOString(),
      };
      await safeSet(`listing:${id}`, JSON.stringify(listing), true);
      const idxRaw = await safeGet("catalog-index", true);
      const idx = idxRaw ? JSON.parse(idxRaw) : [];
      idx.push(id);
      await safeSet("catalog-index", JSON.stringify(idx), true);

      setTitle("");
      setPrice("");
      setFiles([]);
      setPreviews([]);
      setDone(true);
      onListed(listing);
      setTimeout(() => setDone(false), 2500);
    } catch {
      setError("Could not publish the listing. Try again.");
    }
    setBusy(false);
  }

  return (
    <div className="mx-auto max-w-md rounded-2xl bg-[#F6EEDD] p-6 shadow-xl">
      <h2 className="mb-4 text-lg font-bold text-[#24170F]">List an item in your kiduuka</h2>

      <form onSubmit={submitListing} className="flex flex-col gap-4">
        <div 
          onClick={() => inputRef.current?.click()} 
          className="flex cursor-pointer flex-col items-center justify-center gap-2 rounded-2xl border-2 border-dashed border-[#1F4B33]/40 bg-white/60 p-6 text-center hover:bg-white transition"
        >
          <Upload className="h-8 w-8 text-[#1F4B33]" />
          <span className="text-sm font-semibold text-[#24170F]">Tap to attach photos</span>
          <span className="text-xs text-[#8A7A63]">Accepted: {ACCEPTED_EXT.join(", ")}</span>
          <input ref={inputRef} type="file" multiple accept="image/*" className="hidden" onChange={(e) => e.target.files && handleFiles(e.target.files)} />
        </div>

        {previews.length > 0 && (
          <div className="grid grid-cols-4 gap-2">
            {previews.map((src, i) => (
              <div key={i} className="group relative aspect-square overflow-hidden rounded-lg bg-white border border-[#24170F]/10">
                <img src={src} alt={`New listing photo ${i + 1}`} className="h-full w-full object-cover" />
                <button 
                  type="button" 
                  onClick={() => removePreview(i)} 
                  className="absolute right-1 top-1 rounded-full bg-black/60 p-1 text-white opacity-0 transition group-hover:opacity-100"
                >
                  <X className="h-3 w-3" />
                </button>
              </div>
            ))}
          </div>
        )}

        <div>
          <label className="text-xs font-semibold text-[#8A7A63]">Product title</label>
          <input 
            value={title} 
            onChange={(e) => setTitle(e.target.value)} 
            className="mt-1 w-full rounded-lg border-2 border-[#24170F]/15 bg-white px-3 py-2 text-sm outline-none focus:border-[#1F4B33]" 
            placeholder="e.g. Fresh matoke bunch" 
          />
        </div>

        <div>
          <label className="text-xs font-semibold text-[#8A7A63]">Price (UGX)</label>
          <input 
            type="number" 
            inputMode="numeric" 
            value={price} 
            onChange={(e) => setPrice(e.target.value)} 
            className="mt-1 w-full rounded-lg border-2 border-[#24170F]/15 bg-white px-3 py-2 font-[Space_Mono] text-sm outline-none focus:border-[#1F4B33]" 
            placeholder="15000" 
          />
        </div>

        {error && <p className="text-xs font-medium text-[#C1502E]">{error}</p>}
        {done && <p className="text-xs font-medium text-[#1F4B33]">Listed! Buyers can find it in the catalog now.</p>}

        <button 
          type="submit" 
          disabled={busy} 
          className="flex items-center justify-center gap-2 rounded-xl bg-[#1F4B33] py-2.5 text-sm font-bold text-white hover:bg-[#153423] transition"
        >
          {busy && <Loader2 className="h-4 w-4 animate-spin" />}
          Publish listing
        </button>
      </form>
    </div>
  );
}

/* =================================================================
   ACCOUNT PANEL (Cleaned: No Fees Shown Here)
================================================================= */
function AccountPanel({ currentUser, allListings, onLogout, onDeleted, onOpenImage }) {
  const myListings = allListings.filter((l) => l.sellerUsername === currentUser.username);
  const [confirming, setConfirming] = useState(false);
  const [busy, setBusy] = useState(false);

  async function deleteAccount() {
    setBusy(true);
    try {
      for (const listing of myListings) {
        await safeDelete(`listing:${listing.id}`, true);
      }
      const idxRaw = await safeGet("catalog-index", true);
      const idx = idxRaw ? JSON.parse(idxRaw) : [];
      const newIdx = idx.filter((id) => !myListings.some((l) => l.id === id));
      await safeSet("catalog-index", JSON.stringify(newIdx), true);
      await safeDelete(`user:${currentUser.username}`, true);
      const uIdxRaw = await safeGet("users-index", true);
      const uIdx = uIdxRaw ? JSON.parse(uIdxRaw) : [];
      await safeSet("users-index", JSON.stringify(uIdx.filter((u) => u !== currentUser.username)), true);
      await safeDelete("session", false);
      onDeleted(newIdx);
    } catch {
      // best-effort
    }
    setBusy(false);
  }

  return (
    <div className="mx-auto max-w-md rounded-2xl bg-[#F6EEDD] p-6 shadow-xl">
      <div className="flex items-center justify-between border-b border-[#24170F]/10 pb-4">
        <div>
          <h2 className="text-lg font-bold text-[#24170F]">{currentUser.username}</h2>
          <p className="text-xs text-[#8A7A63]">{currentUser.phone || "No contact on file"}</p>
        </div>
        <button onClick={onLogout} className="flex items-center gap-1 rounded-lg bg-[#C1502E]/10 px-3 py-1.5 text-xs font-bold text-[#C1502E] hover:bg-[#C1502E]/20 transition">
          <LogOut className="h-4 w-4" /> Log out
        </button>
      </div>

      <div className="my-6">
        <h3 className="mb-3 text-sm font-bold text-[#24170F]">Your listings ({myListings.length})</h3>

        {myListings.length === 0 ? (
          <p className="py-8 text-center text-xs text-[#8A7A63]">You haven't listed anything yet — head to Sell to add your first item.</p>
        ) : (
          <div className="grid grid-cols-2 gap-3">
            {myListings.map((item) => (
              <div key={item.id} className="cursor-pointer overflow-hidden rounded-xl border-2 border-[#24170F]/10 bg-white" onClick={() => onOpenImage(item, 0)}>
                {item.images?.[0] && (
                  <div className="h-32 w-full bg-[#EFE6D4] overflow-hidden flex items-center justify-center">
                    <img src={item.images[0]} alt={item.title} className="h-full w-full object-cover" />
                  </div>
                )}
                <div className="p-2">
                  <h4 className="line-clamp-1 text-xs font-bold text-[#24170F]">{item.title}</h4>
                  {/* Clean item price view with zero fee info shown in account dashboard */}
                  <p className="font-[Space_Mono] text-xs text-[#C1502E]">{formatUGX(item.price)}</p>
                </div>
              </div>
            ))}
          </div>
        )}
      </div>

      <div className="border-t border-[#24170F]/10 pt-4">
        <h4 className="text-xs font-bold text-[#C1502E]">Danger zone</h4>
        {!confirming ? (
          <button onClick={() => setConfirming(true)} className="mt-2 flex items-center gap-1.5 rounded-lg bg-[#C1502E] px-3 py-2 text-xs font-bold text-white hover:bg-[#a5401f] transition">
            <Trash2 className="h-4 w-4" /> Delete my account
          </button>
        ) : (
          <div className="mt-2 rounded-xl bg-[#C1502E]/10 p-4">
            <p className="text-xs text-[#C1502E]">This permanently removes your account and all listings. This can't be undone.</p>
            <div className="mt-3 flex gap-2">
              <button onClick={deleteAccount} disabled={busy} className="flex items-center gap-1 rounded-lg bg-[#C1502E] px-3 py-1.5 text-xs font-bold text-white hover:bg-[#a5401f] transition">
                {busy && <Loader2 className="h-3 w-3 animate-spin" />} Yes, delete
              </button>
              <button onClick={() => setConfirming(false)} className="rounded-lg border-2 border-[#24170F]/15 px-3 py-1.5 text-xs font-semibold text-[#5b4d3a]">Cancel</button>
            </div>
          </div>
        )}
      </div>
    </div>
  );
}

/* =================================================================
   PACK DRAWER (DISTRIBUTES ORDERS EQUALLY ACROSS RECEIVERS)
================================================================= */
function PackDrawer({ open, onClose, pack, listings, onRemove }) {
  const [contact, setContact] = useState("");
  const [sending, setSending] = useState(false);
  const [result, setResult] = useState(null);

  const items = pack.map((id) => listings.find((l) => l.id === id)).filter(Boolean);
  const total = items.reduce((sum, it) => sum + it.price + calculateFee(it.price), 0);

  async function sendOrder() {
    if (!contact.trim()) {
      setResult({ ok: false, msg: "Add a contact number so the seller can reach you." });
      return;
    }
    if (!items.length) return;

    setSending(true);
    setResult(null);

    const allReceivers = [
      { type: "major", ...RECEIVER_CONFIG.major },
      ...RECEIVER_CONFIG.minors.map((m) => ({ type: "minor", ...m }))
    ];

    const numReceivers = allReceivers.length;
    const itemsPerReceiver = Math.floor(items.length / numReceivers);
    let remainder = items.length % numReceivers;

    let currentIndex = 0;
    const dispatchPromises = allReceivers.map((receiver, index) => {
      const count = itemsPerReceiver + (index < remainder ? 1 : 0);
      const assignedItems = items.slice(currentIndex, currentIndex + count);
      currentIndex += count;

      if (assignedItems.length === 0) return Promise.resolve({ ok: true, receiver: receiver.type });

      const assignedTotal = assignedItems.reduce((sum, it) => sum + it.price + calculateFee(it.price), 0);

      const payload = {
        type: receiver.type === "major" ? "major_full_batch_order" : "minor_assigned_order_split",
        receiverId: receiver.id || "major-hub",
        contact: contact.trim(),
        items: assignedItems.map((it) => ({ id: it.id, title: it.title, price: it.price, sellerUsername: it.sellerUsername })),
        total: assignedTotal,
        submittedAt: new Date().toISOString(),
      };

      return fetch(receiver.url, {
        method: "POST",
        headers: { 
          "Content-Type": "application/json", 
          "X-API-Key": receiver.apiKey 
        },
        body: JSON.stringify(payload),
      })
      .then(res => ({ ok: res.ok, receiver: receiver.type }))
      .catch(() => ({ ok: false, receiver: receiver.type }));
    });

    try {
      const results = await Promise.all(dispatchPromises);
      const majorSuccess = results.find(r => r.receiver === "major")?.ok;
      const successfulCount = results.filter(r => r.ok).length;

      if (majorSuccess && successfulCount >= 2) {
        setResult({ ok: true, msg: "Order items split and successfully dispatched across receiver apps." });
      } else {
        setResult({ ok: false, msg: "Order dispatch failed due to multiple receiver network errors." });
      }
    } catch {
      setResult({ ok: false, msg: "Failed to dispatch order streams to external receivers." });
    }

    setSending(false);
  }

  return (
    <div className={`fixed inset-0 z-45 flex justify-end transition ${open ? "" : "pointer-events-none"}`}>
      <div className={`absolute inset-0 bg-black/50 transition-opacity ${open ? "opacity-100" : "opacity-0"}`} onClick={onClose} />
      <div className={`relative flex h-full w-full max-w-sm flex-col bg-[#F6EEDD] shadow-2xl transition-transform ${open ? "translate-x-0" : "translate-x-full"}`}>
        <div className="flex items-center justify-between border-b border-[#24170F]/10 p-4">
          <h2 className="font-bold text-[#24170F]">Your Pack</h2>
          <button onClick={onClose} className="text-[#8A7A63] hover:text-[#24170F]"><X className="h-5 w-5" /></button>
        </div>

        <div className="flex-1 overflow-y-auto p-4 space-y-3">
          {items.length === 0 ? (
            <p className="py-12 text-center text-xs text-[#8A7A63]">Your pack is empty. Add items from the catalog to bundle them into one order.</p>
          ) : (
            items.map((item) => (
              <div key={item.id} className="flex items-center justify-between rounded-xl bg-white p-3 shadow-sm border border-[#24170F]/10">
                <div className="flex items-center gap-3">
                  {item.images?.[0] && (
                    <div className="h-12 w-12 rounded-lg bg-[#EFE6D4] overflow-hidden flex items-center justify-center shrink-0">
                      <img src={item.images[0]} alt={item.title} className="h-full w-full object-cover" />
                    </div>
                  )}
                  <div>
                    <h4 className="text-xs font-bold text-[#24170F] line-clamp-1">{item.title}</h4>
                    <p className="font-[Space_Mono] text-xs text-[#C1502E]">{formatUGX(item.price)}</p>
                  </div>
                </div>
                <button onClick={() => onRemove(item.id)} className="text-[#8A7A63] hover:text-[#C1502E] p-1">
                  <Trash2 className="h-4 w-4" />
                </button>
              </div>
            ))
          )}
        </div>

        {items.length > 0 && (
          <div className="border-t border-[#24170F]/10 bg-[#EFE6D4] p-4">
            <div className="mb-3 flex justify-between font-bold text-[#24170F]">
              <span>Total (incl. fees)</span>
              <span className="font-[Space_Mono] text-[#C1502E]">{formatUGX(total)}</span>
            </div>
            <input 
              value={contact} 
              onChange={(e) => setContact(e.target.value)} 
              placeholder="Your contact number (07XX XXX XXX)" 
              className="mb-2 w-full rounded-lg border-2 border-[#24170F]/15 bg-white px-3 py-2 text-sm outline-none focus:border-[#1F4B33]" 
            />
            <button 
              onClick={sendOrder} 
              disabled={sending}
              className="flex w-full items-center justify-center gap-2 rounded-xl bg-[#1F4B33] py-2.5 text-xs font-bold text-white hover:bg-[#153423] transition"
            >
              {sending && <Loader2 className="h-4 w-4 animate-spin" />} Send Pack as equal split order
            </button>
            {result && (
              <p className={`mt-2 flex items-center gap-1.5 text-xs font-medium ${result.ok ? "text-[#1F4B33]" : "text-[#C1502E]"}`}>
                {result.ok ? <Check className="h-3.5 w-3.5" /> : <AlertCircle className="h-3.5 w-3.5" />} {result.msg}
              </p>
            )}
          </div>
        )}
      </div>
    </div>
  );
}

/* =================================================================
   MAIN APP
================================================================= */
export default function App() {
  useEffect(() => { ensureFonts(); }, []);
  const [page, setPage] = useState("catalog");
  const [listings, setListings] = useState([]);
  const [loadingCatalog, setLoadingCatalog] = useState(true);
  const [search, setSearch] = useState("");
  const [currentUser, setCurrentUser] = useState(null);
  const [authMode, setAuthMode] = useState(null);
  const [pack, setPack] = useState([]);
  const [packOpen, setPackOpen] = useState(false);
  const [viewer, setViewer] = useState({ item: null, index: null });

  useEffect(() => {
    (async () => {
      setLoadingCatalog(true);
      const idxRaw = await safeGet("catalog-index", true);
      const idx = idxRaw ? JSON.parse(idxRaw) : [];
      if (idx.length) {
        const results = await Promise.all(idx.map((id) => safeGet(`listing:${id}`, true)));
        const parsed = results.filter(Boolean).map((r) => JSON.parse(r));
        setListings(parsed.reverse());
      }
      setLoadingCatalog(false);

      const sessionUser = await safeGet("session", false);
      if (sessionUser) {
        const raw = await safeGet(`user:${sessionUser}`, true);
        if (raw) setCurrentUser(JSON.parse(raw));
      }

      const packRaw = await safeGet("pack", false);
      if (packRaw) {
        try { setPack(JSON.parse(packRaw)); } catch {}
      }
    })();
  }, []);

  const persistPack = useCallback(async (next) => {
    setPack(next);
    await safeSet("pack", JSON.stringify(next), false);
  }, []);

  function addToPack(item) {
    if (pack.includes(item.id)) return;
    persistPack([...pack, item.id]);
  }

  function removeFromPack(id) {
    persistPack(pack.filter((p) => p !== id));
  }

  function openImage(item, index) {
    setViewer({ item, index });
  }

  function handleAuthed(record) {
    setCurrentUser(record);
    setAuthMode(null);
    setPage("account");
  }

  function handleDeleted(newIdx) {
    setListings((prev) => prev.filter((l) => newIdx.includes(l.id)));
    setCurrentUser(null);
    setPage("catalog");
  }

  function handleListed(listing) {
    setListings((prev) => [listing, ...prev]);
  }

  const filtered = listings.filter((l) => l.title.toLowerCase().includes(search.trim().toLowerCase()));

  return (
    <div className="min-h-screen bg-[#F6EEDD] pb-24" style={{ fontFamily: "Inter, sans-serif" }}>
      <header className="bg-[#1F4B33] text-white">
        <div className="mx-auto flex max-w-4xl items-center justify-between p-4">
          <div className="flex items-center gap-2">
            <Store className="h-6 w-6 text-[#E8A93D]" />
            <div>
              <h1 className="text-xs font-bold uppercase tracking-wider text-[#E8A93D]">Johamas Online</h1>
              <span className="text-lg font-extrabold tracking-tight">Kiduuka</span>
            </div>
          </div>

          <div className="flex items-center gap-3">
            <button onClick={() => setPackOpen(true)} className="relative rounded-full bg-white/10 p-2 text-white hover:bg-white/20 transition" aria-label="Open pack">
              <ShoppingBag className="h-5 w-5" />
              {pack.length > 0 && (
                <span className="absolute -right-1 -top-1 flex h-4 w-4 items-center justify-center rounded-full bg-[#C1502E] text-[10px] font-bold">
                  {pack.length}
                </span>
              )}
            </button>

            {currentUser ? (
              <button onClick={() => setPage("account")} className="rounded-full bg-white/10 p-2 text-white hover:bg-white/20 transition" aria-label="Account">
                <User className="h-5 w-5" />
              </button>
            ) : (
              <button onClick={() => setAuthMode("login")} className="rounded-lg bg-white/10 px-3 py-1.5 text-xs font-bold text-white hover:bg-white/20 transition">
                Log in
              </button>
            )}
          </div>
        </div>

        <div className="mx-auto max-w-4xl px-4 pb-4">
          <div className="relative">
            <Search className="absolute left-3 top-1/2 h-4 w-4 -translate-y-1/2 text-[#8A7A63]" />
            <input 
              value={search} 
              onChange={(e) => setSearch(e.target.value)} 
              placeholder="Search the kiduuka..." 
              className="w-full rounded-full bg-white/95 py-2 pl-9 pr-4 text-sm text-[#241B14] outline-none placeholder:text-[#8A7A63]" 
            />
          </div>
        </div>

        <KitengeDivider />
      </header>

      <nav className="mx-auto flex max-w-4xl gap-2 p-4">
        {[
          { id: "catalog", label: "Catalog" },
          { id: "upload", label: "Sell" },
          { id: "account", label: "Account" },
        ].map((t) => (
          <button 
            key={t.id} 
            onClick={() => {
              if (t.id !== "catalog" && !currentUser) {
                setAuthMode("login");
                return;
              }
              setPage(t.id);
            }} 
            className={`rounded-full px-4 py-1.5 text-xs font-bold uppercase tracking-wide transition ${
              page === t.id ? "bg-[#241B14] text-white shadow-sm" : "bg-white text-[#5b4d3a] hover:bg-[#EFE6D4]"
            }`}
          >
            {t.label}
          </button>
        ))}
      </nav>

      <main className="mx-auto max-w-4xl p-4">
        {page === "catalog" && (
          <>
            {loadingCatalog ? (
              <div className="flex justify-center py-16"><Loader2 className="h-8 w-8 animate-spin text-[#1F4B33]" /></div>
            ) : filtered.length === 0 ? (
              <div className="py-16 text-center">
                <p className="text-base font-bold text-[#24170F]">{listings.length === 0 ? "This kiduuka is still empty" : "Nothing matches your search"}</p>
                <p className="text-xs text-[#8A7A63]">{listings.length === 0 ? "Be the first to list an item — tap Sell above." : "Try a different word."}</p>
              </div>
            ) : (
              <div className="grid grid-cols-2 gap-4 sm:grid-cols-3">
                {filtered.map((item) => (
                  <ProductCard 
                    key={item.id} 
                    item={item} 
                    onOpenImage={openImage} 
                    onAddToPack={addToPack} 
                    inPack={pack.includes(item.id)} 
                  />
                ))}
              </div>
            )}
          </>
        )}

        {page === "upload" && currentUser && (
          <UploadPanel currentUser={currentUser} onListed={handleListed} />
        )}

        {page === "account" && currentUser && (
          <AccountPanel 
            currentUser={currentUser} 
            allListings={listings} 
            onLogout={async () => { await safeDelete("session", false); setCurrentUser(null); setPage("catalog"); }} 
            onDeleted={handleDeleted} 
            onOpenImage={openImage} 
          />
        )}
      </main>

      {authMode && (
        <AuthModal 
          mode={authMode} 
          onClose={() => setAuthMode(null)} 
          onSwitchMode={setAuthMode} 
          onAuthed={handleAuthed} 
        />
      )}

      {viewer.item && (
        <ImageViewer 
          images={viewer.item.images} 
          index={viewer.index} 
          onClose={() => setViewer({ item: null, index: null })} 
          onChangeIndex={(i) => setViewer((v) => ({ ...v, index: i }))} 
        />
      )}

      <PackDrawer 
        open={packOpen} 
        onClose={() => setPackOpen(false)} 
        pack={pack} 
        listings={listings} 
        onRemove={removeFromPack} 
      />
    </div>
  );
}
