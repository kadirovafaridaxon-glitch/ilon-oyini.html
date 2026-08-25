
import React, { useState, useMemo } from "react";
import {
  Search, Cpu, MemoryStick, HardDrive, Monitor, Battery, Weight,
  ShoppingCart, X, Check, Zap, Star, Truck, ShieldCheck, ChevronLeft,
} from "lucide-react";

const LAPTOPS = [
  {
    id: "lp-01",
    brand: "ASUS",
    model: "TUF Gaming A15",
    tag: "O'yin uchun",
    price: 12500000,
    oldPrice: 14200000,
    rating: 4.7,
    reviews: 312,
    sold: "1,2 ming",
    accent: "#7A3CFF",
    look: { body: "#16161a", lid: "stripe", lidColor: "#FF7A1A", keys: "rgb" },
    img: "https://images.unsplash.com/photo-1771014817844-327a14245bd1?auto=format&fit=crop&w=800&q=80",
    specs: {
      cpu: "AMD Ryzen 7 7735HS",
      gpu: "RTX 4060 8GB",
      ram: "16GB DDR5",
      storage: "512GB SSD NVMe",
      screen: "15.6\" FHD 144Hz",
      battery: "10 soatgacha",
      weight: "2.2 kg",
    },
    highlight: "144Hz ekran va RTX 4060 — og'ir o'yinlarni ham muammosiz tortadi.",
  },
  {
    id: "lp-02",
    brand: "Lenovo",
    model: "ThinkPad E14",
    tag: "Ish uchun",
    price: 8900000,
    oldPrice: null,
    rating: 4.8,
    reviews: 540,
    sold: "3,4 ming",
    accent: "#E60000",
    look: { body: "#1c1c1c", lid: "plain", lidColor: "#1c1c1c", keys: "normal", dot: true },
    img: "https://images.unsplash.com/photo-1575320854760-bfffc3550640?auto=format&fit=crop&w=800&q=80",
    specs: {
      cpu: "Intel Core i5-1335U",
      gpu: "Intel Iris Xe",
      ram: "16GB DDR4",
      storage: "512GB SSD",
      screen: "14\" FHD IPS",
      battery: "14 soatgacha",
      weight: "1.6 kg",
    },
    highlight: "Mustahkam korpus va uzoq batareya — ofis va safar uchun ideal.",
  },
  {
    id: "lp-03",
    brand: "Apple",
    model: "MacBook Air M3",
    tag: "Professional",
    price: 16200000,
    oldPrice: 17500000,
    rating: 4.9,
    reviews: 890,
    sold: "5,1 ming",
    accent: "#8C8C93",
    look: { body: "#D9D9DE", lid: "plain", lidColor: "#D9D9DE", keys: "minimal", notch: true },
    img: "https://images.unsplash.com/photo-1611186871348-b1ce696e52c9?auto=format&fit=crop&w=800&q=80",
    specs: {
      cpu: "Apple M3 8-core",
      gpu: "M3 10-core GPU",
      ram: "8GB Unified",
      storage: "256GB SSD",
      screen: "13.6\" Liquid Retina",
      battery: "18 soatgacha",
      weight: "1.24 kg",
    },
    highlight: "Shovqinsiz, yupqa va kuchli — dizaynerlar va videografiya uchun sara tanlov.",
  },
  {
    id: "lp-04",
    brand: "HP",
    model: "Pavilion 15",
    tag: "Talabalar uchun",
    price: 6400000,
    oldPrice: 7100000,
    rating: 4.5,
    reviews: 214,
    sold: "980",
    accent: "#0096D6",
    look: { body: "#C7CDD4", lid: "plain", lidColor: "#C7CDD4", keys: "normal" },
    img: "https://images.unsplash.com/photo-1491336440196-6d4fee45a05e?auto=format&fit=crop&w=800&q=80",
    specs: {
      cpu: "Intel Core i3-1215U",
      gpu: "Intel UHD",
      ram: "8GB DDR4",
      storage: "256GB SSD",
      screen: "15.6\" FHD",
      battery: "8 soatgacha",
      weight: "1.75 kg",
    },
    highlight: "Arzon narxda kundalik vazifalar — referat, dars va internet uchun yetarli.",
  },
  {
    id: "lp-05",
    brand: "Dell",
    model: "XPS 13",
    tag: "Professional",
    price: 15800000,
    oldPrice: null,
    rating: 4.8,
    reviews: 176,
    sold: "640",
    accent: "#0672D6",
    look: { body: "#1a1a1c", lid: "plain", lidColor: "#B8BCC2", keys: "minimal" },
    img: "https://images.unsplash.com/photo-1575320854760-bfffc3550640?auto=format&fit=crop&w=800&q=80",
    specs: {
      cpu: "Intel Core i7-1355U",
      gpu: "Intel Iris Xe",
      ram: "16GB LPDDR5",
      storage: "1TB SSD",
      screen: "13.4\" 3.5K OLED",
      battery: "12 soatgacha",
      weight: "1.27 kg",
    },
    highlight: "OLED ekran va premium metall korpus — ko'zni qamashtiruvchi aniqlik.",
  },
  {
    id: "lp-06",
    brand: "Acer",
    model: "Nitro V15",
    tag: "O'yin uchun",
    price: 10200000,
    oldPrice: 11400000,
    rating: 4.6,
    reviews: 402,
    sold: "2,0 ming",
    accent: "#43A047",
    look: { body: "#18181a", lid: "stripe", lidColor: "#43A047", keys: "rgb" },
    img: "https://images.unsplash.com/photo-1771014817844-327a14245bd1?auto=format&fit=crop&w=800&q=80",
    specs: {
      cpu: "Intel Core i5-13420H",
      gpu: "RTX 4050 6GB",
      ram: "16GB DDR5",
      storage: "512GB SSD",
      screen: "15.6\" FHD 144Hz",
      battery: "9 soatgacha",
      weight: "2.1 kg",
    },
    highlight: "Narx-sifat nisbati zo'r gaming noutbuk — o'rta byudjet uchun eng yaxshisi.",
  },
  {
    id: "lp-07",
    brand: "Lenovo",
    model: "IdeaPad Slim 3",
    tag: "Talabalar uchun",
    price: 5600000,
    oldPrice: 6200000,
    rating: 4.4,
    reviews: 128,
    sold: "710",
    accent: "#E60000",
    look: { body: "#CBCDD2", lid: "plain", lidColor: "#CBCDD2", keys: "normal" },
    img: "https://images.unsplash.com/photo-1491336440196-6d4fee45a05e?auto=format&fit=crop&w=800&q=80",
    specs: {
      cpu: "AMD Ryzen 5 7530U",
      gpu: "AMD Radeon Graphics",
      ram: "8GB DDR4",
      storage: "512GB SSD",
      screen: "15.6\" FHD",
      battery: "10 soatgacha",
      weight: "1.65 kg",
    },
    highlight: "Yengil, tez va hamyonbop — birinchi noutbuk sifatida mukammal.",
  },
  {
    id: "lp-08",
    brand: "ASUS",
    model: "Zenbook 14 OLED",
    tag: "Professional",
    price: 13100000,
    oldPrice: null,
    rating: 4.7,
    reviews: 96,
    sold: "350",
    accent: "#7A3CFF",
    look: { body: "#16323A", lid: "spun", lidColor: "#1E5C66", keys: "minimal" },
    img: "https://images.unsplash.com/photo-1611186871348-b1ce696e52c9?auto=format&fit=crop&w=800&q=80",
    specs: {
      cpu: "Intel Core i7-1360P",
      gpu: "Intel Iris Xe",
      ram: "16GB LPDDR5",
      storage: "1TB SSD",
      screen: "14\" 2.8K OLED",
      battery: "13 soatgacha",
      weight: "1.39 kg",
    },
    highlight: "OLED aniqligi va yengil vazni bilan safar va ish uchun teng darajada qulay.",
  },
];

const FILTERS = ["Barchasi", "O'yin uchun", "Ish uchun", "Talabalar uchun", "Professional"];

function formatSum(n) {
  return n.toLocaleString("de-DE") + " so'm";
}

function discountPct(price, oldPrice) {
  if (!oldPrice) return null;
  return Math.round(((oldPrice - price) / oldPrice) * 100);
}

// Illustrated, model-specific laptop "photo" used as a product image.
// Each product carries a `look` descriptor (body color, lid pattern, keyboard style,
// notch/trackpoint dot) so every card renders visibly differently, echoing that
// model's real-world silhouette without reproducing any brand's actual logo artwork.
// Real product photo when available, falling back to the illustrated
// silhouette (below) if the image fails to load.
function ProductImage({ img, accent, brand, look, style }) {
  const [failed, setFailed] = React.useState(false);
  if (img && !failed) {
    return (
      <img
        src={img}
        alt={`${brand} noutbuk fotosi`}
        onError={() => setFailed(true)}
        style={{ width: "100%", height: "100%", objectFit: "cover", borderRadius: 10, ...style }}
      />
    );
  }
  return <LaptopArt accent={accent} brand={brand} look={look} />;
}

function LaptopArt({ accent = "#7A3CFF", brand = "", look = {} }) {
  const {
    body = "#1c1c1e",
    lid = "plain",
    lidColor = body,
    keys = "normal",
    notch = false,
    dot = false,
  } = look;

  const keyboardRows = Array.from({ length: 3 });

  return (
    <svg viewBox="0 0 220 180" width="100%" height="100%" role="img" aria-label={`${brand} noutbuk rasmi`}>
      <ellipse cx="110" cy="158" rx="82" ry="7" fill="#00000010" />

      {/* Lid / back of screen, tilted slightly to suggest a 3/4 product shot */}
      <g>
        <rect x="34" y="14" width="152" height="98" rx="8" fill={lidColor} />
        {lid === "stripe" && (
          <rect x="34" y="14" width="10" height="98" rx="4" fill={accent} opacity="0.9" />
        )}
        {lid === "spun" && (
          <>
            <circle cx="110" cy="63" r="34" fill="none" stroke="#ffffff22" strokeWidth="2" />
            <circle cx="110" cy="63" r="24" fill="none" stroke="#ffffff1a" strokeWidth="2" />
            <circle cx="110" cy="63" r="14" fill="none" stroke="#ffffff14" strokeWidth="2" />
          </>
        )}
        {/* Screen inset */}
        <rect x="44" y="22" width="132" height="82" rx="3" fill="#0b0b0d" />
        <rect x="44" y="22" width="132" height="82" rx="3" fill={accent} opacity="0.16" />
        {notch && <rect x="100" y="22" width="20" height="6" rx="3" fill="#0b0b0d" />}
        {/* Screen content lines */}
        <rect x="56" y="36" width="58" height="6" rx="3" fill={accent} opacity="0.65" />
        <rect x="56" y="48" width="86" height="4.5" rx="2" fill="#ffffff4d" />
        <rect x="56" y="57" width="70" height="4.5" rx="2" fill="#ffffff33" />
        <rect x="56" y="66" width="40" height="4.5" rx="2" fill="#ffffff26" />
      </g>

      {/* Base / keyboard deck, drawn as a trapezoid for a subtle 3D feel */}
      <path d="M20 112 h180 l14 30 a7 7 0 01-7 9 H13 a7 7 0 01-7-9 z" fill={body === lidColor ? shade(body, -6) : body} />
      <path d="M20 112 h180 l4 9 H16 z" fill={shade(body, 8)} opacity="0.5" />

      {/* Keyboard */}
      <g opacity="0.9">
        {keyboardRows.map((_, r) => (
          <g key={r}>
            {Array.from({ length: 10 }).map((_, c) => (
              <rect
                key={c}
                x={44 + c * 13.2}
                y={120 + r * 7.5}
                width="10.5"
                height="5.5"
                rx="1.3"
                fill={
                  keys === "rgb"
                    ? ["#FF5CA0", "#7A3CFF", "#3CD2FF", "#43E97B"][(r + c) % 4]
                    : keys === "minimal"
                    ? "#00000022"
                    : "#ffffff26"
                }
                opacity={keys === "rgb" ? 0.85 : 1}
              />
            ))}
          </g>
        ))}
      </g>

      {/* Trackpad */}
      <rect x="88" y="142" width="44" height="20" rx="3" fill="#00000030" />
      {dot && <circle cx="110" cy="118" r="2.6" fill="#E60000" />}

      {/* Hinge */}
      <rect x="96" y="110" width="28" height="4" rx="2" fill="#00000040" />
    </svg>
  );
}

function shade(hex, amt) {
  const n = parseInt(hex.replace("#", ""), 16);
  let r = (n >> 16) + amt;
  let g = ((n >> 8) & 0xff) + amt;
  let b = (n & 0xff) + amt;
  r = Math.min(255, Math.max(0, r));
  g = Math.min(255, Math.max(0, g));
  b = Math.min(255, Math.max(0, b));
  return `#${((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1)}`;
}

function Stars({ rating }) {
  const full = Math.round(rating);
  return (
    <span style={{ display: "inline-flex", gap: 1 }}>
      {[1, 2, 3, 4, 5].map((i) => (
        <Star
          key={i}
          size={12}
          fill={i <= full ? "#FFB800" : "none"}
          color={i <= full ? "#FFB800" : "#D8D8DC"}
        />
      ))}
    </span>
  );
}

export default function NoutbukDokoni() {
  const [query, setQuery] = useState("");
  const [filter, setFilter] = useState("Barchasi");
  const [selected, setSelected] = useState(null);
  const [cart, setCart] = useState([]);
  const [cartOpen, setCartOpen] = useState(false);
  const [toast, setToast] = useState("");

  const filtered = useMemo(() => {
    return LAPTOPS.filter((l) => {
      const matchesFilter = filter === "Barchasi" || l.tag === filter;
      const q = query.trim().toLowerCase();
      const matchesQuery =
        !q ||
        l.brand.toLowerCase().includes(q) ||
        l.model.toLowerCase().includes(q) ||
        l.specs.cpu.toLowerCase().includes(q);
      return matchesFilter && matchesQuery;
    });
  }, [query, filter]);

  function addToCart(laptop) {
    setCart((c) => [...c, laptop]);
    setToast(`${laptop.brand} ${laptop.model} savatga qo'shildi`);
    setTimeout(() => setToast(""), 1800);
  }

  function removeFromCart(idx) {
    setCart((c) => c.filter((_, i) => i !== idx));
  }

  const total = cart.reduce((s, l) => s + l.price, 0);

  return (
    <div style={styles.page}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;600;700;800&display=swap');
        * { box-sizing: border-box; font-family: 'Manrope', sans-serif; }
        body { margin: 0; }
        .card { transition: box-shadow 0.15s ease, transform 0.15s ease; }
        .card:hover { box-shadow: 0 6px 20px rgba(20,20,30,0.08); transform: translateY(-2px); }
        .pill { transition: all 0.15s ease; }
        .fabbtn:active { transform: scale(0.94); }
        button:focus-visible, input:focus-visible { outline: 2px solid #7A3CFF; outline-offset: 2px; }
        @media (prefers-reduced-motion: reduce) { .card, .pill { transition: none !important; } }
        @media (max-width: 720px) {
          .grid-resp { grid-template-columns: repeat(2, 1fr) !important; }
          .hide-mobile { display: none !important; }
        }
      `}</style>

      {/* Top bar */}
      <header style={styles.header}>
        <div style={styles.headerInner}>
          <div style={styles.logo}>
            noutbuk<span style={{ color: "#7A3CFF" }}>market</span>
          </div>
          <div style={styles.searchWrap}>
            <Search size={17} color="#8C8C93" />
            <input
              style={styles.searchInput}
              placeholder="Noutbuk, brend yoki protsessor qidiring"
              value={query}
              onChange={(e) => setQuery(e.target.value)}
            />
          </div>
          <button style={styles.cartBtn} onClick={() => setCartOpen(true)}>
            <ShoppingCart size={19} color="#1A1A1E" />
            {cart.length > 0 && <span style={styles.cartBadge}>{cart.length}</span>}
          </button>
        </div>
      </header>

      {/* Promo strip */}
      <div style={styles.promo}>
        <div style={styles.promoInner}>
          <Truck size={15} />
          <span>Toshkent bo'ylab bepul yetkazib berish</span>
          <span style={styles.promoDivider} />
          <ShieldCheck size={15} />
          <span>Rasmiy kafolat 12 oy</span>
        </div>
      </div>

      {/* Category pills */}
      <div style={styles.filterBar}>
        <div style={styles.filterRow}>
          {FILTERS.map((f) => (
            <button
              key={f}
              className="pill"
              onClick={() => setFilter(f)}
              style={{ ...styles.pill, ...(filter === f ? styles.pillActive : {}) }}
            >
              {f}
            </button>
          ))}
        </div>
      </div>

      {/* Grid */}
      <section style={styles.gridWrap}>
        <div style={styles.grid} className="grid-resp">
          {filtered.length === 0 && (
            <div style={styles.empty}>Hech narsa topilmadi. Boshqa kalit so'z bilan urinib ko'ring.</div>
          )}
          {filtered.map((l) => {
            const pct = discountPct(l.price, l.oldPrice);
            return (
              <div key={l.id} className="card" style={styles.card} onClick={() => setSelected(l)}>
                <div style={styles.cardImgWrap}>
                  {pct && <span style={styles.discountBadge}>-{pct}%</span>}
                  <ProductImage img={l.img} accent={l.accent} brand={l.brand} look={l.look} />
                </div>
                <div style={styles.cardBody}>
                  <div style={styles.cardTagRow}>
                    <span style={styles.cardTag}>{l.tag}</span>
                  </div>
                  <div style={styles.cardModel}>{l.brand} {l.model}</div>
                  <div style={styles.ratingRow}>
                    <Stars rating={l.rating} />
                    <span style={styles.ratingText}>{l.rating}</span>
                    <span style={styles.reviewText}>({l.reviews})</span>
                  </div>
                  <div style={styles.priceRow}>
                    <span style={styles.price}>{formatSum(l.price)}</span>
                    {l.oldPrice && <span style={styles.oldPrice}>{formatSum(l.oldPrice)}</span>}
                  </div>
                  <div style={styles.soldRow}>{l.sold} marta sotilgan</div>
                  <button
                    className="fabbtn"
                    style={styles.addBtn}
                    onClick={(e) => {
                      e.stopPropagation();
                      addToCart(l);
                    }}
                  >
                    <ShoppingCart size={15} /> Savatga
                  </button>
                </div>
              </div>
            );
          })}
        </div>
      </section>

      {/* Detail modal */}
      {selected && (
        <div style={styles.overlay} onClick={() => setSelected(null)}>
          <div style={styles.detailModal} onClick={(e) => e.stopPropagation()}>
            <div style={styles.detailTopBar}>
              <button style={styles.backBtn} onClick={() => setSelected(null)}>
                <ChevronLeft size={18} /> Orqaga
              </button>
            </div>
            <div style={styles.detailImgWrap}>
              {discountPct(selected.price, selected.oldPrice) && (
                <span style={styles.discountBadge}>
                  -{discountPct(selected.price, selected.oldPrice)}%
                </span>
              )}
              <div style={selected.img ? { width: "100%", height: "100%" } : { width: "70%", maxWidth: 260 }}>
                <ProductImage img={selected.img} accent={selected.accent} brand={selected.brand} look={selected.look} />
              </div>
            </div>
            <div style={styles.detailBody}>
              <span style={styles.cardTag}>{selected.tag}</span>
              <h2 style={styles.detailModel}>{selected.brand} {selected.model}</h2>
              <div style={styles.ratingRow}>
                <Stars rating={selected.rating} />
                <span style={styles.ratingText}>{selected.rating}</span>
                <span style={styles.reviewText}>· {selected.reviews} ta sharh · {selected.sold} sotilgan</span>
              </div>
              <p style={styles.detailHighlight}>{selected.highlight}</p>

              <div style={styles.specGrid}>
                <SpecRow icon={<Cpu size={15} />} label="Protsessor" value={selected.specs.cpu} />
                <SpecRow icon={<Zap size={15} />} label="Video karta" value={selected.specs.gpu} />
                <SpecRow icon={<MemoryStick size={15} />} label="Xotira (RAM)" value={selected.specs.ram} />
                <SpecRow icon={<HardDrive size={15} />} label="Xotira (Disk)" value={selected.specs.storage} />
                <SpecRow icon={<Monitor size={15} />} label="Ekran" value={selected.specs.screen} />
                <SpecRow icon={<Battery size={15} />} label="Batareya" value={selected.specs.battery} />
                <SpecRow icon={<Weight size={15} />} label="Og'irligi" value={selected.specs.weight} />
              </div>

              <div style={styles.detailFooter}>
                <div>
                  <div style={styles.detailPrice}>{formatSum(selected.price)}</div>
                  {selected.oldPrice && <div style={styles.oldPrice}>{formatSum(selected.oldPrice)}</div>}
                </div>
                <button
                  style={styles.addBtnLarge}
                  onClick={() => {
                    addToCart(selected);
                    setSelected(null);
                  }}
                >
                  <ShoppingCart size={16} /> Savatga qo'shish
                </button>
              </div>
            </div>
          </div>
        </div>
      )}

      {/* Cart drawer */}
      {cartOpen && (
        <div style={styles.overlay} onClick={() => setCartOpen(false)}>
          <div style={styles.cartDrawer} onClick={(e) => e.stopPropagation()}>
            <div style={styles.cartHead}>
              <h3 style={{ margin: 0, fontWeight: 800 }}>Savat</h3>
              <button style={styles.closeBtn} onClick={() => setCartOpen(false)}>
                <X size={18} />
              </button>
            </div>
            {cart.length === 0 ? (
              <p style={{ color: "#8C8C93", padding: "24px 4px" }}>Savat bo'sh. Noutbuk tanlab qo'shing.</p>
            ) : (
              <>
                <div style={styles.cartList}>
                  {cart.map((l, i) => (
                    <div key={i} style={styles.cartItem}>
                      <div style={styles.cartItemImg}>
                        <ProductImage img={l.img} accent={l.accent} brand={l.brand} look={l.look} />
                      </div>
                      <div style={{ flex: 1 }}>
                        <div style={styles.cartItemName}>{l.brand} {l.model}</div>
                        <div style={styles.cartItemPrice}>{formatSum(l.price)}</div>
                      </div>
                      <button style={styles.removeBtn} onClick={() => removeFromCart(i)}>
                        <X size={14} />
                      </button>
                    </div>
                  ))}
                </div>
                <div style={styles.cartTotal}>
                  <span>Jami</span>
                  <span style={{ fontWeight: 800, color: "#7A3CFF" }}>{formatSum(total)}</span>
                </div>
                <button style={styles.checkoutBtn}>
                  <Check size={16} /> Buyurtma berish
                </button>
              </>
            )}
          </div>
        </div>
      )}

      {toast && <div style={styles.toast}>{toast}</div>}

      <footer style={styles.footer}>
        noutbukmarket.uz — barcha narxlar taxminiy va faqat namoyish maqsadida
      </footer>
    </div>
  );
}

function SpecRow({ icon, label, value }) {
  return (
    <div style={styles.specRow}>
      <div style={styles.specIcon}>{icon}</div>
      <div>
        <div style={styles.specLabel}>{label}</div>
        <div style={styles.specValue}>{value}</div>
      </div>
    </div>
  );
}

const styles = {
  page: {
    minHeight: "100vh",
    background: "#F3F3F6",
    color: "#1A1A1E",
    paddingBottom: 40,
  },
  header: {
    background: "#fff",
    borderBottom: "1px solid #ECECEF",
    position: "sticky",
    top: 0,
    zIndex: 20,
  },
  headerInner: {
    maxWidth: 1120,
    margin: "0 auto",
    padding: "14px 20px",
    display: "flex",
    alignItems: "center",
    gap: 16,
  },
  logo: { fontWeight: 800, fontSize: 19, whiteSpace: "nowrap" },
  searchWrap: {
    flex: 1,
    display: "flex",
    alignItems: "center",
    gap: 8,
    background: "#F3F3F6",
    borderRadius: 10,
    padding: "9px 14px",
  },
  searchInput: {
    background: "transparent",
    border: "none",
    outline: "none",
    fontSize: 14,
    width: "100%",
    color: "#1A1A1E",
  },
  cartBtn: {
    background: "#F3F3F6",
    border: "none",
    borderRadius: 10,
    width: 40,
    height: 40,
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    cursor: "pointer",
    position: "relative",
    flexShrink: 0,
  },
  cartBadge: {
    position: "absolute",
    top: -4,
    right: -4,
    background: "#7A3CFF",
    color: "#fff",
    fontSize: 10,
    fontWeight: 700,
    borderRadius: 10,
    minWidth: 16,
    height: 16,
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    padding: "0 3px",
  },
  promo: { background: "#F1EBFF" },
  promoInner: {
    maxWidth: 1120,
    margin: "0 auto",
    padding: "7px 20px",
    display: "flex",
    alignItems: "center",
    gap: 8,
    fontSize: 12.5,
    color: "#5B2FBF",
    fontWeight: 600,
    flexWrap: "wrap",
  },
  promoDivider: { width: 1, height: 12, background: "#C9B6F5" },
  filterBar: { maxWidth: 1120, margin: "0 auto", padding: "16px 20px 6px" },
  filterRow: { display: "flex", gap: 8, flexWrap: "wrap" },
  pill: {
    background: "#fff",
    border: "1px solid #E4E4E9",
    color: "#4B4B52",
    padding: "8px 16px",
    borderRadius: 20,
    fontSize: 13.5,
    fontWeight: 600,
    cursor: "pointer",
  },
  pillActive: { background: "#1A1A1E", color: "#fff", borderColor: "#1A1A1E" },
  gridWrap: { maxWidth: 1120, margin: "0 auto", padding: "10px 20px 0" },
  grid: {
    display: "grid",
    gridTemplateColumns: "repeat(auto-fill, minmax(230px, 1fr))",
    gap: 14,
  },
  empty: { color: "#8C8C93", padding: "40px 0", gridColumn: "1/-1", textAlign: "center" },
  card: {
    background: "#fff",
    border: "1px solid #ECECEF",
    borderRadius: 14,
    overflow: "hidden",
    cursor: "pointer",
    display: "flex",
    flexDirection: "column",
  },
  cardImgWrap: {
    background: "#FAFAFB",
    height: 150,
    position: "relative",
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    overflow: "hidden",
  },
  discountBadge: {
    position: "absolute",
    top: 10,
    left: 10,
    background: "#FF3B30",
    color: "#fff",
    fontSize: 11,
    fontWeight: 800,
    padding: "3px 7px",
    borderRadius: 6,
    zIndex: 2,
  },
  cardBody: { padding: "12px 14px 14px", display: "flex", flexDirection: "column", gap: 4, flex: 1 },
  cardTagRow: { marginBottom: 2 },
  cardTag: {
    display: "inline-block",
    background: "#F1EBFF",
    color: "#7A3CFF",
    fontSize: 10.5,
    fontWeight: 700,
    padding: "3px 8px",
    borderRadius: 6,
  },
  cardModel: { fontSize: 14.5, fontWeight: 700, lineHeight: 1.3, minHeight: 38 },
  ratingRow: { display: "flex", alignItems: "center", gap: 4, fontSize: 12 },
  ratingText: { fontWeight: 700 },
  reviewText: { color: "#8C8C93" },
  priceRow: { display: "flex", alignItems: "baseline", gap: 8, marginTop: 4, flexWrap: "wrap" },
  price: { fontSize: 16, fontWeight: 800 },
  oldPrice: { fontSize: 12.5, color: "#B4B4BA", textDecoration: "line-through" },
  soldRow: { fontSize: 11, color: "#B0B0B6" },
  addBtn: {
    marginTop: 8,
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    gap: 6,
    background: "#1A1A1E",
    color: "#fff",
    border: "none",
    padding: "9px 10px",
    borderRadius: 9,
    fontSize: 12.5,
    fontWeight: 700,
    cursor: "pointer",
  },
  overlay: {
    position: "fixed",
    inset: 0,
    background: "rgba(20,20,25,0.45)",
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    zIndex: 50,
    padding: 20,
  },
  detailModal: {
    background: "#fff",
    borderRadius: 16,
    maxWidth: 560,
    width: "100%",
    maxHeight: "88vh",
    overflowY: "auto",
    position: "relative",
  },
  detailTopBar: { padding: "12px 16px 0" },
  backBtn: {
    display: "flex",
    alignItems: "center",
    gap: 4,
    background: "transparent",
    border: "none",
    color: "#4B4B52",
    fontSize: 13.5,
    fontWeight: 600,
    cursor: "pointer",
    padding: 0,
  },
  detailImgWrap: {
    background: "#FAFAFB",
    height: 200,
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    margin: "12px 20px 0",
    borderRadius: 12,
    position: "relative",
    overflow: "hidden",
  },
  detailBody: { padding: 24 },
  detailModel: { fontSize: 24, fontWeight: 800, margin: "8px 0 6px" },
  detailHighlight: { color: "#6B6B72", fontSize: 14, lineHeight: 1.6, margin: "12px 0 20px" },
  specGrid: { display: "grid", gridTemplateColumns: "1fr 1fr", gap: 14, marginBottom: 22 },
  specRow: { display: "flex", gap: 10, alignItems: "flex-start" },
  specIcon: { color: "#7A3CFF", marginTop: 2 },
  specLabel: { fontSize: 11, color: "#8C8C93" },
  specValue: { fontSize: 13.5, fontWeight: 600 },
  detailFooter: {
    display: "flex",
    justifyContent: "space-between",
    alignItems: "center",
    paddingTop: 18,
    borderTop: "1px solid #ECECEF",
  },
  detailPrice: { fontSize: 21, fontWeight: 800 },
  addBtnLarge: {
    display: "flex",
    alignItems: "center",
    gap: 8,
    background: "#7A3CFF",
    color: "#fff",
    border: "none",
    padding: "11px 18px",
    borderRadius: 10,
    fontWeight: 700,
    fontSize: 14,
    cursor: "pointer",
  },
  cartDrawer: {
    background: "#fff",
    borderRadius: 16,
    maxWidth: 420,
    width: "100%",
    maxHeight: "88vh",
    display: "flex",
    flexDirection: "column",
    padding: 20,
  },
  cartHead: { display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 12 },
  closeBtn: { background: "#F3F3F6", border: "none", borderRadius: 8, width: 32, height: 32, cursor: "pointer" },
  cartList: { overflowY: "auto", flex: 1, display: "flex", flexDirection: "column", gap: 10, margin: "8px 0" },
  cartItem: { display: "flex", gap: 10, alignItems: "center" },
  cartItemImg: { width: 56, height: 44, background: "#FAFAFB", borderRadius: 8, flexShrink: 0, padding: 4 },
  cartItemName: { fontSize: 13.5, fontWeight: 700 },
  cartItemPrice: { fontSize: 12, color: "#7A3CFF", fontWeight: 700 },
  removeBtn: { background: "transparent", border: "none", color: "#B0B0B6", cursor: "pointer" },
  cartTotal: {
    display: "flex",
    justifyContent: "space-between",
    padding: "14px 0",
    borderTop: "1px solid #ECECEF",
    fontSize: 15,
    fontWeight: 700,
  },
  checkoutBtn: {
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    gap: 8,
    background: "#7A3CFF",
    color: "#fff",
    border: "none",
    padding: "13px",
    borderRadius: 10,
    fontWeight: 700,
    fontSize: 14,
    cursor: "pointer",
  },
  toast: {
    position: "fixed",
    bottom: 24,
    left: "50%",
    transform: "translateX(-50%)",
    background: "#1A1A1E",
    color: "#fff",
    padding: "10px 18px",
    borderRadius: 10,
    fontSize: 13.5,
    zIndex: 100,
  },
  footer: { textAlign: "center", color: "#B0B0B6", fontSize: 12, marginTop: 30 },
};
