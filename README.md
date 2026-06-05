#[index.html](https://github.com/user-attachments/files/28623575/index.html)
 bio-spark<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Bio-Spark</title>
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
<style>
* { margin:0; padding:0; box-sizing:border-box; font-family:'-apple-system','Noto Sans KR',sans-serif; }
body { background:#f0f2f5; display:flex; justify-content:center; align-items:center; min-height:100vh; }

/* ── 폰 컨테이너 ── */
.phone-container { width:375px; height:812px; background:#fff; border-radius:30px; box-shadow:0 12px 40px rgba(0,0,0,0.15); position:relative; display:flex; flex-direction:column; overflow:hidden; }
.app-header { height:50px; padding:0 20px; display:flex; align-items:center; justify-content:space-between; background:#fff; z-index:10; border-bottom:1px solid #f0f0f0; }
.app-header span { font-size:24px; cursor:pointer; color:#333; }
.app-header .header-title { font-size:16px; font-weight:bold; color:#111; }
.app-content { flex:1; padding:10px 20px 80px; display:flex; flex-direction:column; overflow-y:auto; }
.step-screen { display:none; flex-direction:column; flex:1; }
.step-screen.active { display:flex; }

/* ── 버튼 ── */
.btn-next { width:100%; height:56px; background:#FF6B35; color:#fff; border:none; border-radius:16px; font-size:16px; font-weight:700; cursor:pointer; margin-top:auto; }
.btn-outline { width:100%; height:56px; background:#fff; color:#FF6B35; border:2px solid #FF6B35; border-radius:16px; font-size:16px; font-weight:700; cursor:pointer; margin-top:10px; }
.btn-purple { width:100%; height:52px; background:#7B2FBE; color:#fff; border:none; border-radius:14px; font-size:15px; font-weight:700; cursor:pointer; }
.btn-orange { width:100%; height:52px; background:#FF6B35; color:#fff; border:none; border-radius:14px; font-size:15px; font-weight:700; cursor:pointer; }

/* ── 하단 네비 ── */
.fixed-bottom-nav { position:absolute; bottom:0; width:100%; height:65px; background:#fff; border-top:1px solid #eee; display:none; justify-content:space-around; align-items:center; padding-bottom:5px; z-index:10; }
.nav-button { display:flex; flex-direction:column; align-items:center; color:#888; font-size:10px; cursor:pointer; background:none; border:none; width:20%; }
.nav-button.active { color:#FF6B35; font-weight:bold; }
.nav-button span { font-size:22px; margin-bottom:2px; }

/* ════════════════════════════
   🔥 SPLASH SCREEN
   ════════════════════════════ */
#splash-screen {
  position:absolute; inset:0; z-index:200;
  background:#fff;
  display:flex; flex-direction:column; align-items:center; justify-content:center;
  transition:opacity 0.6s ease;
}
#splash-screen.fade-out { opacity:0; pointer-events:none; }

.splash-glow {
  position:absolute; width:220px; height:220px; border-radius:50%;
  background:radial-gradient(circle, rgba(255,107,53,0.15) 0%, transparent 70%);
  transform:scale(0); transition:transform 1.2s ease;
}
.splash-glow.show { transform:scale(1); }

.splash-flame {
  position:relative; margin-bottom:20px;
  transform:scale(0) translateY(20px);
  opacity:0;
  transition:transform 0.9s cubic-bezier(0.34,1.56,0.64,1), opacity 0.6s ease;
  transform-origin:bottom center;
}
.splash-flame.show { transform:scale(1) translateY(0); opacity:1; }

.flame-svg { filter:drop-shadow(0 0 20px rgba(255,107,53,0.6)); }

.splash-logo {
  opacity:0; transform:translateY(12px);
  transition:opacity 0.6s ease 0.3s, transform 0.6s ease 0.3s;
  text-align:center;
}
.splash-logo.show { opacity:1; transform:translateY(0); }
.splash-logo h1 { font-size:28px; font-weight:900; color:#1A1A1A; letter-spacing:-0.5px; }
.splash-logo p { font-size:11px; color:#FF6B35; letter-spacing:2.5px; margin-top:4px; font-weight:500; }

/* ════════════════════════════
   온보딩
   ════════════════════════════ */
.step-bar-container { display:flex; gap:6px; margin-bottom:30px; margin-top:10px; }
.step-bar { flex:1; height:4px; background:#e0e0e0; border-radius:2px; }
.step-bar.active { background:#FF6B35; }
.title-area h2 { font-size:24px; font-weight:700; line-height:1.4; color:#111; margin-top:10px; }
.title-area p { font-size:14px; color:#888; margin-top:6px; }
.input-center-box { flex:1; display:flex; flex-direction:column; justify-content:center; align-items:center; gap:20px; }
.value-display { font-size:40px; font-weight:800; color:#FF6B35; }
.slider-input { width:100%; accent-color:#FF6B35; height:6px; cursor:pointer; }
.result-box { background:#FFF3EE; border-radius:20px; padding:24px; text-align:center; margin-top:20px; }
.result-title { font-size:14px; color:#666; margin-bottom:8px; }
.result-value { font-size:32px; font-weight:800; color:#FF6B35; }
.bmi-badge { display:inline-block; padding:6px 14px; background:#FF6B35; color:#fff; border-radius:20px; font-size:14px; font-weight:bold; margin-top:10px; }

/* ════════════════════════════
   홈
   ════════════════════════════ */
.main-summary-card { background:linear-gradient(135deg,#FF6B35,#FF8E53); border-radius:24px; padding:24px; color:#fff; box-shadow:0 8px 24px rgba(255,107,53,0.25); margin-bottom:24px; margin-top:10px; }
.summary-header { display:flex; justify-content:space-between; align-items:center; font-size:14px; opacity:0.9; margin-bottom:12px; }
.summary-calorie { font-size:34px; font-weight:800; margin-bottom:16px; }
.progress-container { background:rgba(255,255,255,0.3); border-radius:10px; height:8px; overflow:hidden; }
.progress-bar { background:#fff; height:100%; width:0%; transition:width 0.5s ease-out; }
.section-title { font-size:16px; font-weight:700; color:#222; margin-bottom:12px; display:flex; justify-content:space-between; align-items:center; }
.meal-grid { display:flex; flex-direction:column; gap:12px; margin-bottom:20px; }
.meal-card { background:#f8f9fa; border-radius:16px; padding:16px; display:flex; justify-content:space-between; align-items:center; border:1px solid #eee; }
.meal-info { display:flex; align-items:center; gap:12px; }
.meal-icon-box { width:40px; height:40px; background:#fff; border-radius:12px; display:flex; justify-content:center; align-items:center; color:#FF6B35; box-shadow:0 2px 6px rgba(0,0,0,0.05); }
/* 홈 배너: 프리미엄 서비스 */
.premium-banner { background:linear-gradient(135deg,#7B2FBE,#9C4FE0); border-radius:16px; padding:14px 16px; margin-bottom:16px; display:flex; align-items:center; gap:12px; cursor:pointer; }
.premium-banner-text h4 { font-size:14px; font-weight:700; color:#fff; }
.premium-banner-text p { font-size:11px; color:rgba(255,255,255,0.8); margin-top:2px; }

/* ════════════════════════════
   기록 탭
   ════════════════════════════ */
.method-card { background:#fff; border:1px solid #ddd; border-radius:16px; padding:16px; margin-bottom:10px; display:flex; align-items:center; gap:15px; cursor:pointer; transition:0.2s; }
.method-icon { width:40px; height:40px; background:#f5f5f5; border-radius:10px; display:flex; justify-content:center; align-items:center; color:#555; }
.diary-section { background:#f8f9fa; border-radius:16px; padding:16px; border:1px solid #eee; margin-bottom:20px; }
.condition-group { display:flex; justify-content:space-between; margin:10px 0 14px; }
.condition-btn { flex:1; background:#fff; border:1px solid #e0e0e0; border-radius:10px; padding:8px 0; font-size:18px; cursor:pointer; text-align:center; margin:0 4px; transition:all 0.2s; }
.condition-btn.selected { background:#FFF3EE; border-color:#FF6B35; transform:scale(1.05); }
.diary-input { width:100%; height:60px; border:1px solid #e0e0e0; border-radius:10px; padding:10px; font-size:13px; resize:none; outline:none; }
.diary-item { background:#fff; padding:12px; border-radius:12px; border-left:4px solid #FF6B35; box-shadow:0 2px 6px rgba(0,0,0,0.03); margin-bottom:10px; }
.camera-viewfinder { height:260px; border:3px dashed #FFCA28; border-radius:16px; background:#fafafa; display:flex; flex-direction:column; justify-content:center; align-items:center; margin:20px 0; color:#aaa; position:relative; }
.camera-viewfinder .corner { position:absolute; width:20px; height:20px; border:3px solid #FFCA28; }
.cam-tl{top:10px;left:10px;border-right:none;border-bottom:none;}
.cam-tr{top:10px;right:10px;border-left:none;border-bottom:none;}
.cam-bl{bottom:10px;left:10px;border-right:none;border-top:none;}
.cam-br{bottom:10px;right:10px;border-left:none;border-top:none;}
.action-buttons { display:flex; justify-content:center; gap:20px; margin-bottom:20px; }
.action-btn { display:flex; flex-direction:column; align-items:center; gap:8px; background:none; border:none; font-size:12px; color:#555; cursor:pointer; }
.action-btn .icon-box { width:50px; height:50px; background:#fff; border:1px solid #eee; border-radius:12px; display:flex; justify-content:center; align-items:center; font-size:24px; box-shadow:0 2px 5px rgba(0,0,0,0.05); }
.result-header-card { display:flex; align-items:center; gap:15px; padding:15px; background:#fff; border:1px solid #eee; border-radius:16px; margin-bottom:15px; }
.macro-card { padding:20px; background:#fff; border:1px solid #eee; border-radius:16px; margin-bottom:15px; display:flex; align-items:center; gap:20px; }
.donut-chart { width:70px; height:70px; border-radius:50%; background:conic-gradient(#4CAF50 0% 32%,#2196F3 32% 75%,#FFCA28 75% 100%); }
.macro-legend { font-size:12px; color:#555; line-height:1.8; }
.macro-legend span { display:inline-block; width:8px; height:8px; border-radius:50%; margin-right:5px; }
.warning-box { background:#FFF3E0; border:1px solid #FFE0B2; border-radius:12px; padding:15px; color:#E65100; margin-bottom:15px; }
.solution-card { background:#f8f9fa; border-radius:12px; padding:12px 15px; margin-bottom:10px; display:flex; align-items:center; gap:12px; }
.todo-item { display:flex; justify-content:space-between; align-items:center; padding:15px 0; border-bottom:1px solid #eee; }
.todo-item.done .title { text-decoration:line-through; color:#aaa; }

/* ════════════════════════════
   💊 PREMIUM SERVICE
   ════════════════════════════ */
#tab-premium { padding-bottom:20px; }
.premium-header-card {
  background:linear-gradient(135deg,#7B2FBE,#9C4FE0);
  border-radius:20px; padding:20px; color:#fff; margin-bottom:20px; margin-top:8px;
  text-align:center;
}
.premium-header-card h2 { font-size:20px; font-weight:800; }
.premium-header-card p { font-size:12px; opacity:0.85; margin-top:6px; line-height:1.5; }

.service-card { border-radius:20px; padding:18px; margin-bottom:14px; border:2px solid transparent; }
.service-card.purple { background:#F3E8FF; border-color:#7B2FBE; }
.service-card.orange { background:#FFF5F0; border-color:#FF6B35; }
.service-card-header { display:flex; align-items:center; gap:12px; margin-bottom:10px; }
.service-icon { width:46px; height:46px; border-radius:14px; display:flex; align-items:center; justify-content:center; font-size:22px; }
.service-icon.purple { background:#7B2FBE; }
.service-icon.orange { background:#FF6B35; }
.service-card h3 { font-size:16px; font-weight:800; color:#1A1A1A; }
.service-card .price { font-size:13px; color:#888; }
.service-card .price strong { color:#7B2FBE; font-size:15px; }
.service-card .price strong.org { color:#FF6B35; }
.service-features { list-style:none; margin:10px 0 14px; }
.service-features li { font-size:13px; color:#444; padding:3px 0; display:flex; align-items:center; gap:6px; }
.service-features li::before { content:"●"; color:#7B2FBE; font-size:7px; }
.service-features li.org::before { color:#FF6B35; }
.detail-btn { display:inline-flex; align-items:center; gap:4px; background:rgba(123,47,190,0.1); color:#7B2FBE; border:none; border-radius:20px; padding:7px 14px; font-size:12px; font-weight:600; cursor:pointer; }
.detail-btn.org { background:rgba(255,107,53,0.1); color:#FF6B35; }
.full-package-banner { background:#FFF5F0; border:1px solid #FFD6B8; border-radius:14px; padding:14px 16px; margin-top:4px; }
.full-package-banner h4 { font-size:13px; font-weight:700; color:#FF6B35; margin-bottom:4px; }
.full-package-banner p { font-size:12px; color:#555; line-height:1.6; }

/* ── 영양제 구독 상세 화면 ── */
.ai-analysis-banner {
  background:linear-gradient(135deg,#7B2FBE,#9C4FE0);
  border-radius:18px; padding:16px; color:#fff; margin-bottom:16px;
}
.ai-analysis-banner h4 { font-size:13px; opacity:0.85; margin-bottom:4px; }
.ai-analysis-banner h3 { font-size:16px; font-weight:800; margin-bottom:12px; }
.tag-row { display:flex; flex-wrap:wrap; gap:6px; margin-bottom:10px; }
.tag { background:rgba(255,255,255,0.2); border-radius:20px; padding:5px 12px; font-size:11px; color:#fff; }
.ai-tip { background:rgba(255,255,255,0.15); border-radius:10px; padding:10px 12px; font-size:12px; line-height:1.6; }

.package-option { border-radius:16px; padding:16px; margin-bottom:12px; border:2px solid transparent; cursor:pointer; transition:all 0.2s; }
.package-option.selected-pkg { border-color:#7B2FBE; }
.package-option.basic { background:#F3E8FF; }
.package-option.premium-pkg { background:#FFF5F0; }
.pkg-header { display:flex; justify-content:space-between; align-items:center; margin-bottom:6px; }
.pkg-name { font-size:15px; font-weight:800; }
.pkg-name.purple { color:#7B2FBE; }
.pkg-name.org { color:#FF6B35; }
.pkg-price { font-size:16px; font-weight:900; }
.pkg-price.purple { color:#7B2FBE; }
.pkg-price.org { color:#FF6B35; }
.pkg-desc { font-size:11px; color:#888; margin-bottom:8px; }
.pill-row { display:flex; flex-wrap:wrap; gap:5px; margin-bottom:10px; }
.pill { background:rgba(123,47,190,0.12); color:#7B2FBE; border-radius:20px; padding:4px 10px; font-size:11px; font-weight:600; }
.pill.org { background:rgba(255,107,53,0.12); color:#FF6B35; }
.pkg-badge { background:#7B2FBE; color:#fff; font-size:9px; font-weight:700; padding:2px 7px; border-radius:6px; margin-left:6px; }
.pkg-badge.org { background:#FF6B35; }
.pkg-note { font-size:10px; color:#bbb; text-align:center; margin-top:8px; }

/* ── 구독 완료 화면 ── */
.success-card { background:linear-gradient(135deg,#7B2FBE,#9C4FE0); border-radius:20px; padding:24px; color:#fff; text-align:center; margin-bottom:16px; }
.success-card .check-icon { font-size:40px; margin-bottom:8px; }
.success-card h3 { font-size:18px; font-weight:800; margin-bottom:4px; }
.success-card p { font-size:12px; opacity:0.85; }
.success-pkg-info { background:rgba(255,255,255,0.2); border-radius:12px; padding:10px 14px; margin-top:14px; font-size:13px; }
.delivery-card { background:#fff; border:1px solid #eee; border-radius:16px; padding:16px; }
.delivery-card h4 { font-size:13px; font-weight:700; color:#bbb; margin-bottom:12px; letter-spacing:0.5px; }
.delivery-item { display:flex; justify-content:space-between; align-items:center; padding:10px 0; border-bottom:1px solid #f5f5f5; }
.delivery-item:last-child { border-bottom:none; }
.delivery-item .dname { font-size:14px; font-weight:700; color:#1A1A1A; }
.delivery-badge { background:#F3E8FF; color:#7B2FBE; border-radius:8px; padding:3px 10px; font-size:11px; font-weight:600; }

/* ── AI 트레이너 채팅 화면 ── */
#tab-ai-trainer {
  display:none; flex-direction:column; flex:1; padding:0;
  height:100%;
}
#tab-ai-trainer.active { display:flex; }

.trainer-header { background:#fff; padding:10px 16px 10px; border-bottom:1px solid #f0f0f0; flex-shrink:0; }
.trainer-header-inner { display:flex; align-items:center; gap:10px; }
.trainer-avatar { width:38px; height:38px; border-radius:50%; background:linear-gradient(135deg,#FF6B35,#FF9F5A); display:flex; align-items:center; justify-content:center; flex-shrink:0; }
.trainer-info h4 { font-size:13px; font-weight:700; color:#1A1A1A; }
.trainer-info p { font-size:10px; color:#34A853; display:flex; align-items:center; gap:3px; margin-top:1px; }
.online-dot { width:6px; height:6px; border-radius:50%; background:#34A853; display:inline-block; }
.trainer-chips { display:flex; gap:5px; margin-top:8px; overflow-x:auto; padding-bottom:2px; }
.trainer-chip { background:#F5F5F5; border-radius:20px; padding:3px 9px; font-size:9px; color:#666; white-space:nowrap; flex-shrink:0; }
.trainer-limit-badge { background:#FFF5F0; border-radius:10px; padding:4px 8px; text-align:center; flex-shrink:0; }
.trainer-limit-badge .lnum { font-size:11px; font-weight:700; color:#FF6B35; }
.trainer-limit-badge .lsub { font-size:8px; color:#bbb; }

.chat-messages { flex:1; overflow-y:auto; padding:12px 14px; display:flex; flex-direction:column; gap:10px; }
.msg-row { display:flex; flex-direction:column; }
.msg-row.user { align-items:flex-end; }
.msg-row.ai { align-items:flex-start; }
.msg-bubble-wrap { display:flex; align-items:flex-end; gap:6px; max-width:88%; }
.ai-avatar-sm { width:28px; height:28px; border-radius:50%; background:linear-gradient(135deg,#FF6B35,#FF9F5A); display:flex; align-items:center; justify-content:center; flex-shrink:0; margin-bottom:2px; }
.msg-bubble { border-radius:16px; padding:11px 14px; font-size:12px; line-height:1.65; white-space:pre-wrap; }
.msg-bubble.ai { background:#fff; border-radius:16px 16px 16px 4px; box-shadow:0 1px 6px rgba(0,0,0,0.07); color:#1A1A1A; }
.msg-bubble.user { background:#FF6B35; border-radius:16px 16px 4px 16px; color:#fff; }

.typing-dots { display:flex; gap:4px; align-items:center; padding:11px 14px; background:#fff; border-radius:16px 16px 16px 4px; box-shadow:0 1px 6px rgba(0,0,0,0.07); }
.typing-dot { width:7px; height:7px; border-radius:50%; background:#FF6B35; animation:bounce 1s infinite; }
.typing-dot:nth-child(2){animation-delay:0.2s;}
.typing-dot:nth-child(3){animation-delay:0.4s;}
@keyframes bounce{0%,100%{transform:translateY(0)}50%{transform:translateY(-4px)}}

.quick-questions { padding:6px 14px 8px; flex-shrink:0; }
.quick-label { font-size:9px; color:#bbb; margin-bottom:5px; }
.quick-scroll { display:flex; gap:6px; overflow-x:auto; padding-bottom:2px; }
.quick-btn { background:#FFF5F0; border:1px solid #FFD6B8; border-radius:20px; padding:6px 12px; font-size:10px; color:#FF6B35; cursor:pointer; white-space:nowrap; flex-shrink:0; font-family:inherit; }
.chat-input-area { padding:8px 14px 14px; background:#fff; border-top:1px solid #f0f0f0; flex-shrink:0; }
.chat-input-row { display:flex; gap:8px; align-items:center; }
.chat-input { flex:1; background:#F8F8F6; border:1.5px solid #EBEBEB; border-radius:22px; padding:10px 14px; font-size:12px; outline:none; font-family:inherit; color:#1A1A1A; }
.chat-send-btn { width:38px; height:38px; border-radius:50%; border:none; cursor:pointer; display:flex; align-items:center; justify-content:center; font-size:16px; transition:background 0.2s; flex-shrink:0; }

/* 잠금 카드 */
.lock-card { background:#fff; border-radius:18px; padding:20px 16px; text-align:center; border:1.5px solid #FFD6B8; margin:8px 0; }
.lock-card h4 { font-size:14px; font-weight:700; color:#1A1A1A; margin-bottom:6px; }
.lock-card p { font-size:11px; color:#bbb; line-height:1.7; margin-bottom:14px; }
.lock-price-box { background:#FFF5F0; border-radius:12px; padding:12px 14px; margin-bottom:14px; border:1px solid #FFD6B8; }
.lock-price-box .ptitle { font-size:12px; color:#FF6B35; font-weight:700; }
.lock-price-box .pval { font-size:20px; font-weight:900; color:#1A1A1A; margin:4px 0; }
.lock-price-box .psub { font-size:10px; color:#bbb; }

/* ════════════════════════════
   📔 MONTHLY DIARY
   ════════════════════════════ */
.diary-month-header { text-align:center; font-size:16px; font-weight:700; color:#1A1A1A; margin:10px 0 14px; }
.month-summary { display:flex; justify-content:space-between; background:#fff; border-radius:16px; padding:14px; border:1px solid #eee; box-shadow:0 2px 8px rgba(0,0,0,0.05); margin-bottom:14px; }
.month-stat { text-align:center; }
.month-stat .mval { font-size:18px; font-weight:900; color:#FF6B35; }
.month-stat .mlabel { font-size:9px; color:#bbb; margin-top:2px; }

.sparkline { display:flex; align-items:flex-end; gap:2px; height:28px; margin-bottom:4px; }
.sparkline-bar { flex:1; border-radius:2px; background:#F0F0F0; }
.sparkline-bar.has-data { background:#FF6B35; opacity:0.8; }

.cal-weekdays { display:grid; grid-template-columns:repeat(7,1fr); margin-bottom:6px; }
.cal-weekday { text-align:center; font-size:9px; font-weight:600; color:#bbb; padding-bottom:4px; }
.cal-weekday.sun { color:#EF5350; }
.cal-weekday.sat { color:#4285F4; }

.cal-grid { display:grid; grid-template-columns:repeat(7,1fr); gap:3px; }
.cal-cell { aspect-ratio:1; border-radius:10px; cursor:pointer; display:flex; flex-direction:column; align-items:center; justify-content:center; gap:1px; transition:all 0.15s; position:relative; overflow:hidden; }
.cal-cell.empty { background:transparent; cursor:default; }
.cal-cell.no-data { background:#FAFAFA; border:1.5px solid #F0F0F0; }
.cal-cell.has-meal { background:#FFF5F0; border:1.5px solid #FFD6B8; }
.cal-cell.today { background:#FF6B35; border-color:#FF6B35; }
.cal-cell .cday { font-size:7px; font-weight:600; color:#ccc; }
.cal-cell.has-meal .cday { color:#FF6B35; }
.cal-cell.today .cday { color:#fff; }
.cal-cell .cemoji { font-size:13px; }
.cal-cell .cdot { position:absolute; top:3px; right:3px; width:5px; height:5px; border-radius:50%; background:#4285F4; }

/* 날짜 상세 화면 */
.day-meal-card { background:#fff; border-radius:18px; overflow:hidden; margin-bottom:12px; box-shadow:0 2px 10px rgba(0,0,0,0.06); }
.day-meal-header { height:110px; background:linear-gradient(135deg,#FFF5F0,#FFE8D6); display:flex; align-items:center; justify-content:center; position:relative; }
.day-meal-header .score-badge { position:absolute; top:10px; right:10px; background:#FF6B35; color:#fff; font-size:10px; font-weight:700; padding:3px 8px; border-radius:10px; }
.day-meal-body { padding:12px 14px; }
.day-meal-body h4 { font-size:15px; font-weight:700; color:#1A1A1A; }
.day-meal-body .kcal { font-size:11px; color:#bbb; margin-top:2px; }
.macro-row { display:flex; gap:8px; margin-top:10px; }
.macro-item { flex:1; background:#FAFAFA; border-radius:10px; padding:7px 8px; text-align:center; }
.macro-item .mval { font-size:13px; font-weight:700; }
.macro-item .mlabel { font-size:9px; color:#bbb; }

.mood-card { background:#fff; border-radius:16px; padding:14px; margin-bottom:12px; box-shadow:0 1px 6px rgba(0,0,0,0.04); }
.mood-card h4 { font-size:11px; font-weight:600; color:#bbb; letter-spacing:0.5px; margin-bottom:10px; }
.mood-options { display:flex; gap:8px; }
.mood-btn { flex:1; text-align:center; padding:8px 4px; border-radius:12px; cursor:pointer; transition:all 0.2s; background:#FAFAFA; border:1.5px solid #F0F0F0; }
.mood-btn.active { background:#FFF5F0; border-color:#FF6B35; }
.mood-btn .memoji { font-size:20px; }
.mood-btn .mlabel { font-size:8px; color:#bbb; margin-top:3px; }
.mood-btn.active .mlabel { color:#FF6B35; }

.day-diary-card { background:#fff; border-radius:16px; padding:14px; margin-bottom:12px; box-shadow:0 1px 6px rgba(0,0,0,0.04); }
.day-diary-card h4 { font-size:11px; font-weight:600; color:#bbb; letter-spacing:0.5px; margin-bottom:10px; }
.diary-text { font-size:12px; color:#333; line-height:1.7; min-height:60px; }
.diary-textarea { width:100%; min-height:80px; background:#FAFAFA; border:1.5px solid #EBEBEB; border-radius:10px; padding:10px; font-size:12px; color:#333; outline:none; font-family:inherit; resize:vertical; line-height:1.6; }
.save-diary-btn { width:100%; background:#FF6B35; color:#fff; border:none; border-radius:12px; padding:12px 0; font-size:13px; font-weight:700; cursor:pointer; margin-top:10px; }

/* ════════════════════════════
   기타
   ════════════════════════════ */
.report-grid { display:grid; grid-template-columns:1fr 1fr; gap:12px; margin-top:15px; }
.report-item { background:#f9f9f9; border:1px solid #eee; border-radius:14px; padding:16px; }
.circle-progress { width:120px; height:120px; border-radius:50%; border:8px solid #FF6B35; display:flex; justify-content:center; align-items:center; margin:0 auto; font-size:28px; font-weight:bold; color:#111; position:relative; }
.circle-progress::after { content:"🔥"; position:absolute; bottom:-10px; right:-10px; font-size:32px; }

#loadingOverlay { display:none; position:absolute; top:0; left:0; width:100%; height:100%; background:rgba(255,255,255,0.92); z-index:100; flex-direction:column; justify-content:center; align-items:center; }
.spinner { border:4px solid #f3f3f3; border-top:4px solid #FF6B35; border-radius:50%; width:40px; height:40px; animation:spin 1s linear infinite; margin-bottom:15px; }
@keyframes spin{0%{transform:rotate(0deg)}100%{transform:rotate(360deg)}}

/* 스크롤바 */
.app-content::-webkit-scrollbar,.chat-messages::-webkit-scrollbar { width:3px; }
.app-content::-webkit-scrollbar-thumb,.chat-messages::-webkit-scrollbar-thumb { background:#FF6B3533; border-radius:3px; }
</style>
</head>
<body>
<div class="phone-container">

  <!-- 🔥 SPLASH -->
  <div id="splash-screen">
    <div class="splash-glow" id="splashGlow"></div>
    <div class="splash-flame" id="splashFlame">
      <svg class="flame-svg" width="80" height="96" viewBox="0 0 60 78" fill="none">
        <path d="M30 76C12 76 4 60 4 46C4 30 14 22 20 12C23 7 26 2 30 0C30 10 35 15 38 20C41 14 41 9 38 4C48 12 56 26 56 42C56 60 48 76 30 76Z" fill="#FF4500"/>
        <path d="M30 68C20 68 16 58 16 50C16 40 22 34 26 26C27.5 22 28.5 18 30 16C30 22 33 26 36 29C38 25 38 21 36 18C43 24 47 33 47 43C47 57 40 68 30 68Z" fill="#FF8C00"/>
        <path d="M30 58C24 58 21 52 21 47C21 41 25 37 27 32C27.8 29 28.5 27 30 26C30 30 32 33 34 35C35 32 35 29 34 27C38 31 40 37 40 44C40 52 36 58 30 58Z" fill="#FFF3E0" opacity="0.95"/>
      </svg>
    </div>
    <div class="splash-logo" id="splashLogo">
      <h1>Bio-Spark</h1>
      <p>대사 인텔리전스</p>
    </div>
  </div>

  <div class="app-header">
    <span class="material-icons" id="backBtn" onclick="prevStep()" style="visibility:hidden;">arrow_back</span>
    <div class="header-title" id="headerTitle">기본 정보 등록</div>
    <span class="material-icons" id="rightIcon" style="visibility:hidden;">notifications_none</span>
  </div>

  <div id="loadingOverlay" style="display:none;">
    <div class="spinner"></div>
    <h3 style="color:#333;font-size:16px;">AI가 음식을 분석중입니다...</h3>
  </div>

  <div class="app-content" id="appContent">

    <!-- 온보딩 진행 바 -->
    <div class="step-bar-container" id="infoStepBar">
      <div class="step-bar active"></div>
      <div class="step-bar"></div>
      <div class="step-bar"></div>
      <div class="step-bar"></div>
    </div>

    <!-- 온보딩 1: 나이 -->
    <div id="step-age" class="step-screen active">
      <div class="title-area">
        <h2>나이를<br>선택해주세요.</h2>
        <p>정확한 기초대사량 계산을 위해 필요합니다.</p>
      </div>
      <div class="input-center-box">
        <div class="value-display" id="ageTxt">25세</div>
        <input type="range" class="slider-input" min="10" max="80" value="25" oninput="document.getElementById('ageTxt').innerText=this.value+'세'">
      </div>
      <button class="btn-next" onclick="nextOnboardingStep(2)">다음</button>
    </div>

    <!-- 온보딩 2: 키 -->
    <div id="step-height" class="step-screen">
      <div class="title-area">
        <h2>신장(키)을<br>선택해주세요.</h2>
        <p>BMI 지수를 계산하는 기준이 됩니다.</p>
      </div>
      <div class="input-center-box">
        <div class="value-display" id="heightTxt">170cm</div>
        <input type="range" class="slider-input" min="130" max="210" value="170" oninput="document.getElementById('heightTxt').innerText=this.value+'cm'">
      </div>
      <button class="btn-next" onclick="nextOnboardingStep(3)">다음</button>
    </div>

    <!-- 온보딩 3: 몸무게 -->
    <div id="step-weight" class="step-screen">
      <div class="title-area">
        <h2>몸무게를<br>선택해주세요.</h2>
        <p>현재 상태를 기반으로 칼로리를 측정합니다.</p>
      </div>
      <div class="input-center-box">
        <div class="value-display" id="weightTxt">60kg</div>
        <input type="range" class="slider-input" min="30" max="140" value="60" oninput="document.getElementById('weightTxt').innerText=this.value+'kg'">
      </div>
      <button class="btn-next" onclick="calculateAndShowResult()">분석하기</button>
    </div>

    <!-- 온보딩 4: 결과 -->
    <div id="step-result" class="step-screen">
      <div class="title-area">
        <h2>대사 분석 리포트</h2>
        <p>입력하신 정보를 바탕으로 맞춤 계산된 결과입니다.</p>
      </div>
      <div style="flex:1;display:flex;flex-direction:column;justify-content:center;gap:16px;">
        <div class="result-box">
          <div class="result-title">나의 BMI 지수</div>
          <div class="result-value" id="bmiResult">20.8</div>
          <div class="bmi-badge" id="bmiStatus">정상 체중</div>
        </div>
        <div class="result-box" style="background:#FFF9F5;">
          <div class="result-title">하루 권장 섭취 칼로리</div>
          <div class="result-value" style="color:#E65100;" id="calorieResult">1,950 kcal</div>
        </div>
      </div>
      <button class="btn-next" onclick="goToDashboard()">Bio-Spark 홈으로 가기</button>
    </div>

    <!-- ══ 홈 탭 ══ -->
    <div id="tab-home" class="step-screen">
      <div class="main-summary-card">
        <div class="summary-header">
          <span>하루 권장 목표</span>
          <span class="material-icons">local_fire_department</span>
        </div>
        <div class="summary-calorie" id="dbCalorieTarget">0 kcal</div>
        <div style="display:flex;justify-content:space-between;font-size:12px;margin-bottom:6px;opacity:0.9;">
          <span>현재 기록: 0 kcal</span>
          <span id="dbCaloriePercent">0% 달성</span>
        </div>
        <div class="progress-container">
          <div class="progress-bar" id="dbProgressBar"></div>
        </div>
      </div>

      <!-- 프리미엄 배너 -->
      <div class="premium-banner" onclick="openPremium()">
        <span style="font-size:26px;">✨</span>
        <div class="premium-banner-text" style="flex:1;">
          <h4>프리미엄 서비스</h4>
          <p>영양제 배송 · AI 헬스 트레이너</p>
        </div>
        <span class="material-icons" style="color:rgba(255,255,255,0.7);font-size:20px;">chevron_right</span>
      </div>

      <div class="section-title"><span>오늘의 식단 기록</span></div>
      <div class="meal-grid">
        <div class="meal-card">
          <div class="meal-info">
            <div class="meal-icon-box"><span class="material-icons">wb_twilight</span></div>
            <div><div class="meal-name" style="font-weight:600;font-size:14px;">아침 식사</div><div style="font-size:12px;color:#aaa;">기록 추가 대기중</div></div>
          </div>
          <span class="material-icons" style="color:#FF6B35;">add_circle_outline</span>
        </div>
        <div class="meal-card">
          <div class="meal-info">
            <div class="meal-icon-box"><span class="material-icons">wb_sunny</span></div>
            <div><div style="font-weight:600;font-size:14px;">점심 식사</div><div style="font-size:12px;color:#aaa;">기록 추가 대기중</div></div>
          </div>
          <span class="material-icons" style="color:#FF6B35;">add_circle_outline</span>
        </div>
      </div>
    </div>

    <!-- ══ 기록 탭 메인 ══ -->
    <div id="tab-record-main" class="step-screen">
      <div class="title-area" style="margin-bottom:15px;">
        <h2>어떤 방법으로<br>기록할까요?</h2>
      </div>
      <div class="method-card" onclick="startCameraFlow()">
        <div class="method-icon"><span class="material-icons">photo_camera</span></div>
        <div style="flex:1;"><h4 style="font-size:15px;color:#222;margin-bottom:3px;">사진으로 기록</h4><p style="font-size:12px;color:#888;">음식 사진을 찍어 분석해요.</p></div>
        <span class="material-icons" style="color:#ccc;">chevron_right</span>
      </div>
      <div class="method-card" onclick="alert('직접 입력 기능은 준비중입니다.')">
        <div class="method-icon"><span class="material-icons">edit</span></div>
        <div style="flex:1;"><h4 style="font-size:15px;color:#222;margin-bottom:3px;">직접 입력</h4><p style="font-size:12px;color:#888;">음식을 검색하여 입력해요.</p></div>
        <span class="material-icons" style="color:#ccc;">chevron_right</span>
      </div>
      <hr style="border:0;height:1px;background:#eee;margin:15px 0;">
      <div class="section-title"><span>📝 오늘의 대사 다이어리</span></div>
      <div class="diary-section">
        <p style="font-size:13px;color:#555;">지금 내 컨디션 상태는?</p>
        <div class="condition-group">
          <button class="condition-btn selected" onclick="selectCondition(this,'😄 좋음')">😄</button>
          <button class="condition-btn" onclick="selectCondition(this,'😐 보통')">😐</button>
          <button class="condition-btn" onclick="selectCondition(this,'🥱 피곤')">🥱</button>
          <button class="condition-btn" onclick="selectCondition(this,'🤢 속더룸')">🤢</button>
        </div>
        <textarea class="diary-input" id="diaryMemo" placeholder="오늘 식단 후의 몸 상태나 가벼운 일기를 남겨보세요..."></textarea>
        <button class="btn-next" style="height:40px;border-radius:10px;font-size:14px;margin-top:10px;" onclick="saveDiary()">다이어리 저장하기</button>
      </div>
      <div id="diaryHistory" style="display:flex;flex-direction:column;gap:10px;padding-bottom:20px;">
        <div class="diary-item">
          <div style="display:flex;justify-content:space-between;font-size:12px;color:#888;margin-bottom:4px;">
            <span>상태: 😄 좋음</span><span>방금 전</span>
          </div>
          <div style="font-size:14px;color:#333;">오늘 아침 샐러드 먹었더니 속이 편안함!</div>
        </div>
      </div>
    </div>

    <!-- 기록: 카메라 -->
    <div id="tab-record-camera" class="step-screen">
      <div class="camera-viewfinder">
        <div class="corner cam-tl"></div><div class="corner cam-tr"></div>
        <div class="corner cam-bl"></div><div class="corner cam-br"></div>
        <span class="material-icons" style="font-size:40px;margin-bottom:10px;">restaurant</span>
        <p style="font-size:14px;">음식을 사각형 안에 맞춰주세요</p>
      </div>
      <div class="action-buttons">
        <button class="action-btn"><div class="icon-box"><span class="material-icons">photo_camera</span></div>촬영</button>
        <button class="action-btn"><div class="icon-box"><span class="material-icons">insert_photo</span></div>갤러리</button>
      </div>
      <button class="btn-next" onclick="triggerAIAnalysis()">AI 분석 시작</button>
    </div>

    <!-- 기록: 결과 -->
    <div id="tab-record-result" class="step-screen">
      <div class="result-header-card">
        <div style="width:50px;height:50px;background:#f5f5f5;border-radius:12px;display:flex;justify-content:center;align-items:center;">
          <span class="material-icons" style="color:#aaa;">restaurant_menu</span>
        </div>
        <div>
          <h4 style="font-size:16px;color:#111;">닭가슴살 샐러드</h4>
          <p style="font-size:13px;color:#888;margin-top:3px;">530 kcal · 점심 기록</p>
        </div>
      </div>
      <div class="macro-card">
        <div class="donut-chart"></div>
        <div class="macro-legend">
          <div><span style="background:#4CAF50;"></span>탄수화물 32%</div>
          <div><span style="background:#2196F3;"></span>단백질 43%</div>
          <div><span style="background:#FFCA28;"></span>지방 25%</div>
        </div>
      </div>
      <div class="warning-box">
        <h4 style="display:flex;align-items:center;gap:5px;font-size:14px;margin-bottom:5px;"><span class="material-icons">warning_amber</span>혈당 스파이크 주의</h4>
        <p style="font-size:12px;margin-top:5px;">당 지수가 높은 소스가 포함되어 혈당이 빠르게 상승할 수 있어요!</p>
      </div>
      <div class="solution-card">
        <span class="material-icons" style="color:#7B2FBE;">medication</span>
        <div><h5 style="font-size:13px;color:#333;">영양제 추천</h5><p style="font-size:11px;color:#888;">비타민B, 마그네슘 → <span style="color:#7B2FBE;cursor:pointer;" onclick="openPremium()">구독 배송 신청</span></p></div>
      </div>
      <div class="solution-card">
        <span class="material-icons" style="color:#2196F3;">directions_run</span>
        <div><h5 style="font-size:13px;color:#333;">운동 추천</h5><p style="font-size:11px;color:#888;">식후 20분 걷기 추천</p></div>
      </div>
      <button class="btn-next" style="margin-top:20px;" onclick="goToTodo()">To-do 리스트에 추가</button>
    </div>

    <!-- 기록: To-do -->
    <div id="tab-record-todo" class="step-screen">
      <div style="text-align:center;margin:20px 0;">
        <p style="font-size:13px;color:#888;margin-bottom:10px;">오늘의 성취율</p>
        <div class="circle-progress">60%</div>
      </div>
      <div style="margin-top:20px;">
        <div class="todo-item done">
          <div><div class="title" style="font-weight:bold;font-size:15px;">점심 식사 기록</div><div style="font-size:12px;color:#888;">530kcal</div></div>
          <span class="material-icons" style="color:#4CAF50;">check_box</span>
        </div>
        <div class="todo-item">
          <div><div style="font-weight:bold;font-size:15px;color:#111;">비타민B 섭취</div><div style="font-size:12px;color:#888;">식후 20분 이내</div></div>
          <span class="material-icons" style="color:#ddd;">check_box_outline_blank</span>
        </div>
        <div class="todo-item">
          <div><div style="font-weight:bold;font-size:15px;color:#111;">20분 걷기</div><div style="font-size:12px;color:#888;">식후 20분 이내</div></div>
          <span class="material-icons" style="color:#ddd;">check_box_outline_blank</span>
        </div>
      </div>
      <button class="btn-next" style="margin-top:30px;" onclick="goToScore()">오늘의 대사결과 확인</button>
    </div>

    <!-- 기록: 점수 -->
    <div id="tab-record-score" class="step-screen">
      <div style="background:#fff;border-radius:24px;padding:40px 20px;text-align:center;border:1px solid #eee;box-shadow:0 10px 30px rgba(0,0,0,0.05);margin-top:20px;">
        <div style="font-size:16px;color:#555;font-weight:bold;">오늘의 대사 점수</div>
        <div style="margin-top:20px;">
          <h1 style="font-size:60px;color:#FF6B35;font-weight:900;">85<span style="font-size:30px;color:#888;">/100</span></h1>
        </div>
        <div style="font-size:50px;margin:20px 0;text-shadow:0 4px 10px rgba(255,107,53,0.4);">🔥 🔥 🔥</div>
        <div style="display:flex;justify-content:space-between;align-items:center;margin-top:30px;border-top:2px solid #f5f5f5;padding-top:20px;">
          <span style="font-weight:bold;color:#333;">대사 레벨</span>
          <span style="font-weight:bold;color:#FF6B35;font-size:20px;">Lv.7</span>
        </div>
      </div>
      <p style="text-align:center;font-size:14px;color:#555;margin-top:20px;line-height:1.5;">오늘 대사가 활활 타오르고 있어요!🔥</p>
      <button class="btn-outline" style="margin-top:30px;" onclick="switchTab('home',document.querySelectorAll('.nav-button')[0],'Bio-Spark')">홈으로 돌아가기</button>
    </div>

    <!-- ══ 💊 프리미엄 서비스 메인 ══ -->
    <div id="tab-premium" class="step-screen">
      <div style="font-size:12px;color:#aaa;margin:8px 0 4px;line-height:1.6;">Bio-Spark 앱 데이터를 기반으로<br>더 정밀한 건강 관리를 시작해보세요.</div>

      <!-- 영양제 카드 -->
      <div class="service-card purple" onclick="openSupplementDetail()">
        <div class="service-card-header">
          <div class="service-icon purple">💊</div>
          <div>
            <h3>맞춤 영양제 구독 배송</h3>
            <div class="price">월 구독료 <strong>₩29,000~</strong></div>
          </div>
        </div>
        <ul class="service-features">
          <li>AI 식단 분석 기반 자동 조합</li>
          <li>혈당 대사 타입별 맞춤 성분 추천</li>
          <li>매달 식단에 맞게 구성 변경</li>
        </ul>
        <button class="detail-btn" onclick="event.stopPropagation();openSupplementDetail()">자세히 보기 →</button>
      </div>

      <!-- AI 트레이너 카드 -->
      <div class="service-card orange" onclick="openAITrainer()">
        <div class="service-card-header">
          <div class="service-icon orange">🤖</div>
          <div>
            <h3>AI 헬스 트레이너</h3>
            <div class="price">무료 3회 이후 <strong class="org">₩9,900</strong></div>
          </div>
        </div>
        <ul class="service-features">
          <li class="org">실시간 식단 혈당 데이터 연동 상담</li>
          <li class="org">운동 영양제 식단 통합 조언</li>
          <li class="org">24시간 언제든 무제한 즉시 답변</li>
        </ul>
        <button class="detail-btn org" onclick="event.stopPropagation();openAITrainer()">지금 상담하기 →</button>
      </div>

      <!-- 풀패키지 배너 -->
      <div class="full-package-banner">
        <h4>🔥 풀 패키지 혜택</h4>
        <p>영양제 배송 + AI 트레이너를 함께 이용하면<br>월 <strong style="color:#FF6B35;">₩39,000~</strong> · 대사 관리 올인원 패키지</p>
      </div>
    </div>

    <!-- ══ 영양제 구독 상세 ══ -->
    <div id="tab-supplement-detail" class="step-screen">
      <!-- AI 분석 배너 -->
      <div class="ai-analysis-banner">
        <h4>🤖 AI 식단 분석 결과</h4>
        <h3>이번 달 내 식단 패턴</h3>
        <div class="tag-row">
          <span class="tag">오트밀 &amp; 베리 (탄수화물)</span>
          <span class="tag">닭가슴살 랩 (단백질)</span>
          <span class="tag">오일 파스타 (탄수화물)</span>
        </div>
        <div class="ai-tip">🍀 탄수화물 과다 패턴 감지 → <strong>비타민 B군 + 마그네슘</strong> 우선 추천</div>
      </div>

      <div style="font-size:13px;font-weight:700;color:#1A1A1A;margin-bottom:10px;">구독 패키지 선택</div>

      <!-- 베이직 패키지 -->
      <div class="package-option basic selected-pkg" id="pkgBasic" onclick="selectPackage('basic')">
        <div class="pkg-header">
          <div><span class="pkg-name purple">베이직 패키지</span><span class="pkg-badge">인기</span></div>
          <div class="pkg-price purple">₩29,000<span style="font-size:11px;font-weight:400;color:#888;">/월 3종</span></div>
        </div>
        <div class="pkg-desc">탄수화물 대사 + 혈당 케어 기본 조합</div>
        <div class="pill-row">
          <span class="pill">비타민 B군</span>
          <span class="pill">오메가-3</span>
          <span class="pill">마그네슘</span>
        </div>
        <button class="btn-purple" onclick="event.stopPropagation();subscribePackage('basic')">베이직 패키지 구독하기</button>
      </div>

      <!-- 프리미엄 패키지 -->
      <div class="package-option premium-pkg" id="pkgPremium" onclick="selectPackage('premium')">
        <div class="pkg-header">
          <div><span class="pkg-name org">프리미엄 패키지</span><span class="pkg-badge org">추천</span></div>
          <div class="pkg-price org">₩39,000<span style="font-size:11px;font-weight:400;color:#888;">/월 6종</span></div>
        </div>
        <div class="pkg-desc">대사 최적화 풀 스택 조합</div>
        <div class="pill-row">
          <span class="pill org">비타민 B군</span>
          <span class="pill org">오메가-3</span>
          <span class="pill org">마그네슘</span>
          <span class="pill org">아연</span>
          <span class="pill org">유산균</span>
          <span class="pill org">밀크씨슬</span>
        </div>
        <button class="btn-orange" onclick="event.stopPropagation();subscribePackage('premium')">프리미엄 패키지 구독하기</button>
      </div>

      <div class="pkg-note">첫달 무료 이용 가능 · 결제 후 일주일 내 무료 취소 가능</div>
    </div>

    <!-- ══ 구독 완료 ══ -->
    <div id="tab-subscribe-done" class="step-screen">
      <div class="success-card">
        <div class="check-icon">✅</div>
        <h3>구독 신청 완료!</h3>
        <p>다음달 1일 첫 배송 예정이에요!</p>
        <div class="success-pkg-info" id="successPkgInfo">베이직 패키지 3종 · ₩29,000 /월</div>
      </div>
      <div class="delivery-card">
        <h4>이번달 배송구성</h4>
        <div id="deliveryItems"></div>
      </div>
      <button class="btn-next" style="margin-top:16px;" onclick="openPremium()">프리미엄 서비스로 돌아가기</button>
    </div>

    <!-- ══ 🤖 AI 트레이너 ══ -->
    <div id="tab-ai-trainer">
      <div class="trainer-header">
        <div class="trainer-header-inner">
          <div class="trainer-avatar">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
              <path d="M12 2C12 2 7 7.5 7 13C7 15.76 9.24 18 12 18C14.76 18 17 15.76 17 13C17 7.5 12 2 12 2Z" fill="white" opacity=".3"/>
              <path d="M12 5C12 5 8.5 9.5 8.5 13C8.5 14.93 10.07 16.5 12 16.5C13.93 16.5 15.5 14.93 15.5 13C15.5 9.5 12 5 12 5Z" fill="white" opacity=".7"/>
              <path d="M12 8.5C12 8.5 10 11.5 10 13C10 14.1 10.9 15 12 15C13.1 15 14 14.1 14 13C14 11.5 12 8.5 12 8.5Z" fill="white"/>
            </svg>
          </div>
          <div class="trainer-info" style="flex:1;">
            <h4>스파크 AI 트레이너</h4>
            <p><span class="online-dot"></span>온라인 · 대사 데이터 연동중</p>
          </div>
          <div class="trainer-limit-badge" id="trainerLimitBadge">
            <div class="lnum">무료 3회</div>
            <div class="lsub">남음</div>
          </div>
        </div>
        <div class="trainer-chips">
          <span class="trainer-chip">🔥 대사 72점</span>
          <span class="trainer-chip">🩸 점심 후 혈당 스파이크 반복</span>
          <span class="trainer-chip">📅 3일 연속</span>
        </div>
      </div>

      <div class="chat-messages" id="chatMessages">
        <div class="msg-row ai">
          <div class="msg-bubble-wrap">
            <div class="ai-avatar-sm">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="none"><path d="M12 2C12 2 7 7.5 7 13C7 15.76 9.24 18 12 18C14.76 18 17 15.76 17 13C17 7.5 12 2 12 2Z" fill="white" opacity=".3"/><path d="M12 5C12 5 8.5 9.5 8.5 13C8.5 14.93 10.07 16.5 12 16.5C13.93 16.5 15.5 14.93 15.5 13C15.5 9.5 12 5 12 5Z" fill="white" opacity=".7"/><path d="M12 8.5C12 8.5 10 11.5 10 13C10 14.1 10.9 15 12 15C13.1 15 14 14.1 14 13C14 11.5 12 8.5 12 8.5Z" fill="white"/></svg>
            </div>
            <div class="msg-bubble ai">안녕하세요, 민지님! 저는 Bio-Spark AI 트레이너 스파크예요. 🔥

오늘 대사 점수 72점, 연속 3일 기록 중이시네요! 점심 후 혈당 스파이크 패턴이 감지됐는데, 오늘 어떤 부분이 궁금 하신가요?</div>
          </div>
        </div>
      </div>

      <div class="quick-questions" id="quickQuestions">
        <div class="quick-label">빠른 질문</div>
        <div class="quick-scroll">
          <button class="quick-btn" onclick="sendQuickMsg('오늘 점심 먹고 뭐하면 좋을까요?')">오늘 점심 먹고 뭐하면 좋을까요?</button>
          <button class="quick-btn" onclick="sendQuickMsg('혈당 스파이크 줄이는 방법이요')">혈당스파이크 줄이는 방법</button>
          <button class="quick-btn" onclick="sendQuickMsg('지금 영양제 뭐 먹어야 해요?')">지금 영양제 추천</button>
          <button class="quick-btn" onclick="sendQuickMsg('오늘 운동 추천해주세요')">운동 추천</button>
        </div>
      </div>

      <div class="chat-input-area">
        <div class="chat-input-row">
          <input class="chat-input" id="chatInput" placeholder="식단, 운동, 영양제 뭐든 물어보세요..." onkeydown="if(event.key==='Enter')sendChat()">
          <button class="chat-send-btn" id="sendBtn" onclick="sendChat()" style="background:#FF6B35;color:#fff;">↑</button>
        </div>
      </div>
    </div>

    <!-- ══ 📔 먼슬리 다이어리 ══ -->
    <div id="tab-monthly-diary" class="step-screen">
      <div class="diary-month-header">📔 4월 식단 다이어리</div>

      <!-- 월간 요약 -->
      <div class="month-summary">
        <div class="month-stat"><div class="mval">14</div><div class="mlabel">기록일</div></div>
        <div class="month-stat"><div class="mval">88</div><div class="mlabel">평균점수</div></div>
        <div class="month-stat"><div class="mval">1,240</div><div class="mlabel">평균kcal</div></div>
        <div class="month-stat"><div class="mval">5</div><div class="mlabel">일기수</div></div>
      </div>

      <!-- 스파크라인 -->
      <div style="background:#fff;border-radius:14px;padding:12px 14px;margin-bottom:12px;border:1px solid #eee;">
        <div style="font-size:10px;color:#bbb;margin-bottom:6px;">칼로리 기록 추이</div>
        <div class="sparkline" id="sparkline"></div>
        <div style="display:flex;justify-content:space-between;font-size:8px;color:#ccc;margin-top:3px;"><span>1일</span><span>15일</span><span>30일</span></div>
      </div>

      <!-- 달력 -->
      <div style="background:#fff;border-radius:16px;padding:14px 12px;border:1px solid #eee;margin-bottom:12px;">
        <div class="cal-weekdays">
          <div class="cal-weekday sun">일</div>
          <div class="cal-weekday">월</div>
          <div class="cal-weekday">화</div>
          <div class="cal-weekday">수</div>
          <div class="cal-weekday">목</div>
          <div class="cal-weekday">금</div>
          <div class="cal-weekday sat">토</div>
        </div>
        <div class="cal-grid" id="calGrid"></div>
        <div style="display:flex;gap:12px;margin-top:10px;font-size:9px;color:#bbb;">
          <div style="display:flex;align-items:center;gap:4px;"><div style="width:8px;height:8px;border-radius:2px;background:#FFF5F0;border:1px solid #FFD6B8;"></div>식사 기록</div>
          <div style="display:flex;align-items:center;gap:4px;"><div style="width:6px;height:6px;border-radius:50%;background:#4285F4;"></div>일기 작성</div>
        </div>
      </div>
    </div>

    <!-- ══ 날짜 상세 ══ -->
    <div id="tab-day-detail" class="step-screen">
      <div id="dayDetailContent"></div>
    </div>

    <!-- ══ MY ══ -->
    <div id="tab-my" class="step-screen">
      <div style="display:flex;align-items:center;gap:15px;padding:20px 0;border-bottom:1px solid #eee;">
        <span class="material-icons" style="font-size:55px;color:#ddd;">account_circle</span>
        <div>
          <h4 style="font-size:18px;color:#111;">대사 데이터 도전자</h4>
          <p style="font-size:13px;color:#888;margin-top:3px;">목표: 대사 속도 밸런스 유지</p>
        </div>
      </div>
      <div style="margin-top:15px;">
        <p style="padding:15px 0;border-bottom:1px solid #f5f5f5;font-size:15px;cursor:pointer;">체중 및 피트니스 목표 변경</p>
        <p style="padding:15px 0;border-bottom:1px solid #f5f5f5;font-size:15px;cursor:pointer;" onclick="openPremium()">✨ 프리미엄 서비스</p>
        <p style="padding:15px 0;border-bottom:1px solid #f5f5f5;font-size:15px;cursor:pointer;">1:1 개발자 지원실</p>
      </div>
    </div>

    <!-- ══ 배틀 ══ -->
    <div id="tab-battle" class="step-screen">
      <div style="background:#FF6B35;color:#fff;border-radius:14px;padding:18px;margin-bottom:20px;font-weight:bold;text-align:center;">🔥 실시간 대사 소모 배틀방</div>
      <div style="padding:14px 5px;display:flex;justify-content:space-between;border-bottom:1px solid #f5f5f5;"><span>🥇 1위 홍길동</span><strong>98점 (완료)</strong></div>
      <div style="padding:14px 5px;display:flex;justify-content:space-between;border-bottom:1px solid #f5f5f5;"><span>🥈 2위 김철수</span><strong>82점 (진행중)</strong></div>
      <button class="btn-outline" style="margin-top:20px;">초대 코드 생성</button>
    </div>

    <!-- ══ 리포트 ══ -->
    <div id="tab-report" class="step-screen">
      <h4 style="font-size:16px;margin-bottom:5px;text-align:center;color:#444;">🎉 이번 주 종합 분석 레포트</h4>
      <div class="report-grid">
        <div class="report-item"><div>평균 식단 점수</div><div style="font-weight:700;">85 / 100점</div></div>
        <div class="report-item"><div>스파이크 감소율</div><div style="font-weight:700;">최근 3회 다운 📉</div></div>
        <div class="report-item"><div>목표 달성 일수</div><div style="font-weight:700;">주간 5일 성공</div></div>
        <div class="report-item"><div>최종 건강 등급</div><div style="font-weight:700;color:#FF6B35;">우수 (A)</div></div>
      </div>
    </div>

  </div><!-- /app-content -->

  <!-- 하단 네비 -->
  <div class="fixed-bottom-nav" id="mainBottomNav">
    <button class="nav-button active" onclick="switchTab('home',this,'Bio-Spark')"><span class="material-icons">home</span>홈</button>
    <button class="nav-button" onclick="switchTab('record',this,'식단 기록하기')"><span class="material-icons">restaurant</span>기록</button>
    <button class="nav-button" onclick="switchTab('monthly-diary',this,'다이어리')"><span class="material-icons">calendar_month</span>다이어리</button>
    <button class="nav-button" onclick="switchTab('premium',this,'프리미엄 서비스')"><span class="material-icons">star</span>프리미엄</button>
    <button class="nav-button" onclick="switchTab('my',this,'마이페이지')"><span class="material-icons">person</span>MY</button>
  </div>

</div><!-- /phone-container -->

<script>
/* ══════════════════════════════════════════
   🔥 SPLASH
   ══════════════════════════════════════════ */
window.addEventListener('load', () => {
  const splash = document.getElementById('splash-screen');
  const glow   = document.getElementById('splashGlow');
  const flame  = document.getElementById('splashFlame');
  const logo   = document.getElementById('splashLogo');

  setTimeout(() => glow.classList.add('show'), 200);
  setTimeout(() => flame.classList.add('show'), 400);
  setTimeout(() => logo.classList.add('show'), 1200);
  setTimeout(() => {
    splash.classList.add('fade-out');
    setTimeout(() => { splash.style.display='none'; updateOnboardingUI(); }, 650);
  }, 2800);
});

/* ══════════════════════════════════════════
   온보딩
   ══════════════════════════════════════════ */
let globalCalorie = 0;
let currentOnboardingStep = 1;
let currentRecordFlow = 'main';
let selectedConditionText = '😄 좋음';

const backBtn      = document.getElementById('backBtn');
const headerTitle  = document.getElementById('headerTitle');
const rightIcon    = document.getElementById('rightIcon');
const mainBottomNav= document.getElementById('mainBottomNav');
const infoStepBar  = document.getElementById('infoStepBar');

function nextOnboardingStep(step) { currentOnboardingStep=step; updateOnboardingUI(); }

function prevStep() {
  if(mainBottomNav.style.display !== 'flex') {
    if(currentOnboardingStep > 1) { currentOnboardingStep--; updateOnboardingUI(); }
  } else {
    if(currentRecordFlow==='camera') startRecordMain();
    else if(currentRecordFlow==='result') startCameraFlow();
    else if(currentRecordFlow==='todo') goToResult();
    else hideAllAndShow('tab-'+currentPrimaryTab);
  }
}

function updateOnboardingUI() {
  ['step-age','step-height','step-weight','step-result'].forEach((id,i) => {
    document.getElementById(id).style.display = (i===currentOnboardingStep-1)?'flex':'none';
  });
  document.querySelectorAll('.step-bar').forEach((b,i) => {
    i < currentOnboardingStep ? b.classList.add('active') : b.classList.remove('active');
  });
  if(currentOnboardingStep===4) {
    headerTitle.innerText='분석 결과'; backBtn.style.visibility='hidden';
  } else {
    headerTitle.innerText='기본 정보 등록';
    backBtn.style.visibility = currentOnboardingStep>1 ? 'visible' : 'hidden';
  }
}

function calculateAndShowResult() {
  const age    = parseInt(document.getElementById('ageTxt').innerText);
  const height = parseInt(document.getElementById('heightTxt').innerText);
  const weight = parseInt(document.getElementById('weightTxt').innerText);
  const bmi    = (weight/((height/100)**2)).toFixed(1);
  document.getElementById('bmiResult').innerText = bmi;
  let st = bmi<18.5?'저체중':bmi<23?'정상 체중':bmi<25?'과체중':'비만';
  document.getElementById('bmiStatus').innerText = st;
  globalCalorie = Math.round((10*weight+6.25*height-5*age+5)*1.35);
  document.getElementById('calorieResult').innerText = globalCalorie.toLocaleString()+' kcal';
  currentOnboardingStep=4; updateOnboardingUI();
}

function goToDashboard() {
  document.getElementById('dbCalorieTarget').innerText = globalCalorie.toLocaleString()+' kcal';
  ['step-age','step-height','step-weight','step-result'].forEach(id => document.getElementById(id).style.display='none');
  infoStepBar.style.display='none';
  backBtn.style.visibility='hidden';
  rightIcon.style.visibility='visible';
  mainBottomNav.style.display='flex';
  document.getElementById('tab-home').style.display='flex';
  headerTitle.innerText='Bio-Spark';
  initCalendar(); initSparkline();
  setTimeout(() => {
    document.getElementById('dbProgressBar').style.width='35%';
    document.getElementById('dbCaloriePercent').innerText='35% 달성';
  }, 300);
}

/* ══════════════════════════════════════════
   탭 전환
   ══════════════════════════════════════════ */
const ALL_SCREENS = [
  'tab-home','tab-record-main','tab-record-camera','tab-record-result',
  'tab-record-todo','tab-record-score','tab-my','tab-battle','tab-report',
  'tab-premium','tab-supplement-detail','tab-subscribe-done',
  'tab-ai-trainer','tab-monthly-diary','tab-day-detail'
];
let currentPrimaryTab = 'home';

function hideAll() {
  ALL_SCREENS.forEach(id => { const el=document.getElementById(id); if(el) el.style.display='none'; });
}

function showScreen(id) {
  const el = document.getElementById(id);
  if(el) el.style.display='flex';
}

function switchTab(tabName, element, titleText) {
  hideAll();
  document.querySelectorAll('.nav-button').forEach(b => b.classList.remove('active'));
  if(element) element.classList.add('active');
  headerTitle.innerText = titleText;
  backBtn.style.visibility='hidden';

  if(tabName==='record') { startRecordMain(); return; }
  if(tabName==='monthly-diary') { showScreen('tab-monthly-diary'); currentPrimaryTab='monthly-diary'; return; }
  if(tabName==='premium') { showScreen('tab-premium'); currentPrimaryTab='premium'; return; }

  currentPrimaryTab = tabName;
  showScreen('tab-'+tabName);
}

/* ══════════════════════════════════════════
   기록 플로우
   ══════════════════════════════════════════ */
function startRecordMain() {
  hideAll(); currentRecordFlow='main';
  showScreen('tab-record-main');
  headerTitle.innerText='식단 기록하기'; backBtn.style.visibility='hidden';
  currentPrimaryTab='record-main';
}
function startCameraFlow() {
  hideAll(); currentRecordFlow='camera';
  showScreen('tab-record-camera');
  headerTitle.innerText='사진으로 분석'; backBtn.style.visibility='visible';
}
function triggerAIAnalysis() {
  const ov=document.getElementById('loadingOverlay');
  ov.style.display='flex';
  setTimeout(()=>{ ov.style.display='none'; goToResult(); }, 2000);
}
function goToResult() {
  hideAll(); currentRecordFlow='result';
  showScreen('tab-record-result');
  headerTitle.innerText='분석 결과'; backBtn.style.visibility='visible';
}
function goToTodo() {
  hideAll(); currentRecordFlow='todo';
  showScreen('tab-record-todo');
  headerTitle.innerText='오늘의 To-Do'; backBtn.style.visibility='visible';
}
function goToScore() {
  hideAll(); currentRecordFlow='score';
  showScreen('tab-record-score');
  headerTitle.innerText='수고했어요!'; backBtn.style.visibility='hidden';
}

/* ══════════════════════════════════════════
   다이어리 (기록 탭)
   ══════════════════════════════════════════ */
function selectCondition(btn, text) {
  document.querySelectorAll('.condition-btn').forEach(b=>b.classList.remove('selected'));
  btn.classList.add('selected'); selectedConditionText=text;
}
function saveDiary() {
  const t=document.getElementById('diaryMemo').value.trim();
  if(!t) return alert('내용을 입력해주세요!');
  const h=document.getElementById('diaryHistory');
  const d=document.createElement('div'); d.className='diary-item';
  d.innerHTML=`<div style="display:flex;justify-content:space-between;font-size:12px;color:#888;margin-bottom:4px;"><span>상태: ${selectedConditionText}</span><span>방금 전</span></div><div style="font-size:14px;color:#333;">${t}</div>`;
  h.insertBefore(d,h.firstChild);
  document.getElementById('diaryMemo').value='';
  alert('다이어리가 저장되었습니다!');
}

/* ══════════════════════════════════════════
   💊 프리미엄 서비스
   ══════════════════════════════════════════ */
function openPremium() {
  hideAll();
  showScreen('tab-premium');
  headerTitle.innerText='프리미엄 서비스';
  backBtn.style.visibility='visible';
  backBtn.onclick=()=>{ hideAll(); showScreen('tab-home'); headerTitle.innerText='Bio-Spark'; backBtn.style.visibility='hidden'; document.querySelectorAll('.nav-button')[0].classList.add('active'); };
}

function openSupplementDetail() {
  hideAll();
  showScreen('tab-supplement-detail');
  headerTitle.innerText='프리미엄 서비스';
  backBtn.style.visibility='visible';
  backBtn.onclick=()=>openPremium();
}

function selectPackage(pkg) {
  document.getElementById('pkgBasic').classList.toggle('selected-pkg', pkg==='basic');
  document.getElementById('pkgPremium').classList.toggle('selected-pkg', pkg==='premium');
}

function subscribePackage(pkg) {
  const isBasic = pkg==='basic';
  document.getElementById('successPkgInfo').innerText = isBasic
    ? '베이직 패키지 3종 · ₩29,000 /월'
    : '프리미엄 패키지 6종 · ₩39,000 /월';

  const items = isBasic
    ? ['비타민 B군','오메가-3','마그네슘']
    : ['비타민 B군','오메가-3','마그네슘','아연','유산균','밀크씨슬'];
  const container = document.getElementById('deliveryItems');
  container.innerHTML = items.map(n=>
    `<div class="delivery-item"><span class="dname">• ${n}</span><span class="delivery-badge">배송예정</span></div>`
  ).join('');

  hideAll();
  showScreen('tab-subscribe-done');
  headerTitle.innerText='프리미엄 서비스';
  backBtn.style.visibility='visible';
  backBtn.onclick=()=>openSupplementDetail();
}

/* ══════════════════════════════════════════
   🤖 AI 트레이너
   ══════════════════════════════════════════ */
let chatMsgCount = 0;
const FREE_LIMIT = 3;
let isUnlocked = false;

function openAITrainer() {
  hideAll();
  const el = document.getElementById('tab-ai-trainer');
  el.style.display='flex';
  headerTitle.innerText='스파크 AI 트레이너';
  backBtn.style.visibility='visible';
  backBtn.onclick=()=>openPremium();
}

async function sendChat() {
  const input = document.getElementById('chatInput');
  const text = input.value.trim();
  if(!text) return;
  sendMessage(text);
  input.value='';
}

function sendQuickMsg(text) {
  document.getElementById('quickQuestions').style.display='none';
  sendMessage(text);
}

async function sendMessage(text) {
  if(!isUnlocked && chatMsgCount >= FREE_LIMIT) return;

  appendMsg('user', text);
  chatMsgCount++;
  updateLimitBadge();

  const typingId = appendTyping();

  try {
    const res = await fetch('https://api.anthropic.com/v1/messages', {
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body: JSON.stringify({
        model:'claude-sonnet-4-20250514',
        max_tokens:1000,
        system:`당신은 Bio-Spark 앱의 AI 헬스 트레이너 "스파크(Spark)"입니다.
사용자 데이터: 이름=민지, BMI=22.5, 대사점수=72, 목표=혈당관리+체지방감소, 오늘식사=아침오트밀320kcal+점심닭가슴살랩480kcal, 혈당트렌드=점심후스파이크반복, 연속기록=3일
규칙: 한국어로만, 3-4문장 간결하게, 사용자 데이터 반드시 언급, 이모지 적절히 사용, 존댓말`,
        messages:[{role:'user',content:text}]
      })
    });
    const data = await res.json();
    removeTyping(typingId);
    const reply = data.content?.[0]?.text || '죄송해요, 잠시 후 다시 시도해주세요.';
    appendMsg('ai', reply);
  } catch(e) {
    removeTyping(typingId);
    appendMsg('ai','네트워크 오류가 발생했어요. 잠시 후 다시 시도해주세요 🙏');
  }

  if(!isUnlocked && chatMsgCount >= FREE_LIMIT) showLockCard();
}

function appendMsg(role, text) {
  const msgs = document.getElementById('chatMessages');
  const row = document.createElement('div');
  row.className = `msg-row ${role}`;
  if(role==='ai') {
    row.innerHTML=`<div class="msg-bubble-wrap"><div class="ai-avatar-sm"><svg width="14" height="14" viewBox="0 0 24 24" fill="none"><path d="M12 2C12 2 7 7.5 7 13C7 15.76 9.24 18 12 18C14.76 18 17 15.76 17 13C17 7.5 12 2 12 2Z" fill="white" opacity=".3"/><path d="M12 5C12 5 8.5 9.5 8.5 13C8.5 14.93 10.07 16.5 12 16.5C13.93 16.5 15.5 14.93 15.5 13C15.5 9.5 12 5 12 5Z" fill="white" opacity=".7"/><path d="M12 8.5C12 8.5 10 11.5 10 13C10 14.1 10.9 15 12 15C13.1 15 14 14.1 14 13C14 11.5 12 8.5 12 8.5Z" fill="white"/></svg></div><div class="msg-bubble ai">${text}</div></div>`;
  } else {
    row.innerHTML=`<div class="msg-bubble user">${text}</div>`;
  }
  msgs.appendChild(row);
  msgs.scrollTop = msgs.scrollHeight;
}

function appendTyping() {
  const msgs = document.getElementById('chatMessages');
  const id = 'typing-'+Date.now();
  const row = document.createElement('div');
  row.className='msg-row ai'; row.id=id;
  row.innerHTML=`<div class="msg-bubble-wrap"><div class="ai-avatar-sm"><svg width="14" height="14" viewBox="0 0 24 24" fill="none"><path d="M12 2C12 2 7 7.5 7 13C7 15.76 9.24 18 12 18C14.76 18 17 15.76 17 13C17 7.5 12 2 12 2Z" fill="white" opacity=".3"/></svg></div><div class="typing-dots"><div class="typing-dot"></div><div class="typing-dot"></div><div class="typing-dot"></div></div></div>`;
  msgs.appendChild(row); msgs.scrollTop=msgs.scrollHeight;
  return id;
}
function removeTyping(id) { const el=document.getElementById(id); if(el) el.remove(); }

function updateLimitBadge() {
  const badge = document.getElementById('trainerLimitBadge');
  const rem = Math.max(0, FREE_LIMIT-chatMsgCount);
  if(isUnlocked) { badge.innerHTML='<div class="lnum" style="color:#34A853;">∞</div><div class="lsub">프리미엄</div>'; return; }
  badge.innerHTML=`<div class="lnum">무료 ${rem}회</div><div class="lsub">남음</div>`;
}

function showLockCard() {
  const msgs = document.getElementById('chatMessages');
  const lock = document.createElement('div');
  lock.className='lock-card';
  lock.innerHTML=`
    <div style="font-size:28px;margin-bottom:8px;">🔒</div>
    <h4>무료 상담 ${FREE_LIMIT}회 소진</h4>
    <p>프리미엄으로 업그레이드하면<br>AI 트레이너와 무제한 대화 가능해요</p>
    <div class="lock-price-box">
      <div class="ptitle">Spark Premium</div>
      <div class="pval">₩9,900 / 월</div>
      <div class="psub">AI 트레이너 무제한 + 영양제 추천</div>
    </div>
    <button class="btn-next" style="margin-top:0;height:46px;font-size:13px;" onclick="unlockPremium()">프리미엄 시작하기</button>
    <div style="font-size:9px;color:#ccc;margin-top:8px;">첫 달 무료 체험 · 언제든 해지 가능</div>
  `;
  msgs.appendChild(lock); msgs.scrollTop=msgs.scrollHeight;

  const inputEl = document.getElementById('chatInput');
  inputEl.placeholder='프리미엄 업그레이드 후 이용 가능';
  inputEl.disabled=true;
  document.getElementById('sendBtn').style.background='#E0E0E0';
}

function unlockPremium() {
  isUnlocked=true;
  document.querySelectorAll('.lock-card').forEach(el=>el.remove());
  const inputEl=document.getElementById('chatInput');
  inputEl.placeholder='식단, 운동, 영양제 뭐든 물어보세요...';
  inputEl.disabled=false;
  document.getElementById('sendBtn').style.background='#FF6B35';
  updateLimitBadge();
  appendMsg('ai','프리미엄으로 업그레이드 완료! 🎉 이제 무제한으로 상담드릴게요. 무엇이 궁금하신가요?');
}

/* ══════════════════════════════════════════
   📔 먼슬리 다이어리
   ══════════════════════════════════════════ */
const MEALS = {
  1:{emoji:'🥣',name:'오트밀 & 베리',kcal:320,score:92,macro:{c:'45g',p:'12g',f:'8g'},diary:'오늘 처음으로 아침을 빠지지 않고 먹었다! 속이 편안하고 에너지가 충만한 느낌.',mood:'😊'},
  2:{emoji:'🍗',name:'닭가슴살 랩',kcal:480,score:88,macro:{c:'38g',p:'35g',f:'16g'},diary:'점심 기록 성공 🎉 혈당도 안정적으로 유지됐어.',mood:'😊'},
  5:{emoji:'🍳',name:'스크램블 에그',kcal:280,score:85,macro:{c:'12g',p:'22g',f:'18g'},diary:'',mood:'😐'},
  7:{emoji:'🍱',name:'현미 도시락',kcal:520,score:80,macro:{c:'55g',p:'28g',f:'14g'},diary:'현미밥이 생각보다 포만감이 좋다.',mood:'😊'},
  9:{emoji:'🥑',name:'아보카도 토스트',kcal:350,score:90,macro:{c:'32g',p:'10g',f:'22g'},diary:'',mood:'😐'},
  11:{emoji:'🍜',name:'미역국+현미밥',kcal:430,score:83,macro:{c:'52g',p:'18g',f:'8g'},diary:'',mood:'😴'},
  14:{emoji:'🥩',name:'스테이크 샐러드',kcal:560,score:78,macro:{c:'20g',p:'45g',f:'28g'},diary:'스테이크 먹고 나서 좀 무거운 느낌. 다음엔 양 조절 필요.',mood:'😴'},
  16:{emoji:'🍳',name:'두부 스크램블',kcal:300,score:91,macro:{c:'18g',p:'24g',f:'14g'},diary:'두부로 단백질 보충! 가볍고 좋았어.',mood:'😊'},
  18:{emoji:'🐟',name:'연어 포케',kcal:490,score:94,macro:{c:'38g',p:'32g',f:'18g'},diary:'연어 먹고 기분 최고. 몸이 가벼워진 것 같다 🐟',mood:'😊'},
  20:{emoji:'🥗',name:'퀴노아 샐러드',kcal:390,score:89,macro:{c:'42g',p:'18g',f:'12g'},diary:'',mood:'😐'},
  22:{emoji:'🍗',name:'닭가슴살 구이',kcal:320,score:87,macro:{c:'8g',p:'38g',f:'10g'},diary:'',mood:'😊'},
  25:{emoji:'🥣',name:'그릭요거트 볼',kcal:260,score:93,macro:{c:'28g',p:'18g',f:'6g'},diary:'상큼하고 가벼운 아침. 기분 좋음!',mood:'😊'},
  27:{emoji:'🍱',name:'잡곡밥+나물',kcal:410,score:86,macro:{c:'58g',p:'16g',f:'8g'},diary:'',mood:'😐'},
};
const DIARY_DAYS = new Set([1,7,14,16,18,25]);

function initSparkline() {
  const el = document.getElementById('sparkline');
  if(!el) return;
  el.innerHTML='';
  for(let d=1;d<=30;d++){
    const bar=document.createElement('div');
    bar.className='sparkline-bar';
    const m=MEALS[d];
    if(m){ bar.classList.add('has-data'); bar.style.height=Math.round((m.kcal/600)*28)+'px'; }
    else bar.style.height='3px';
    el.appendChild(bar);
  }
}

function initCalendar() {
  const grid=document.getElementById('calGrid');
  if(!grid) return;
  grid.innerHTML='';
  const startOffset=2; // 4월 2025: 화요일 시작
  for(let i=0;i<startOffset;i++){
    const e=document.createElement('div'); e.className='cal-cell empty'; grid.appendChild(e);
  }
  for(let d=1;d<=30;d++){
    const cell=document.createElement('div');
    const m=MEALS[d];
    cell.className='cal-cell '+(m?'has-meal':'no-data')+(d===27?' today':'');
    cell.innerHTML=`<span class="cday">${d}</span>${m?`<span class="cemoji">${m.emoji}</span>`:''}${DIARY_DAYS.has(d)?'<div class="cdot"></div>':''}`;
    cell.onclick=()=>openDayDetail(d);
    grid.appendChild(cell);
  }
}

function openDayDetail(day) {
  const meal=MEALS[day];
  const hasDiary=DIARY_DAYS.has(day);
  let html='';

  if(meal){
    html+=`
      <div class="day-meal-card">
        <div class="day-meal-header">
          <span style="font-size:52px;">${meal.emoji}</span>
          <div class="score-badge">점수 ${meal.score}</div>
        </div>
        <div class="day-meal-body">
          <h4>${meal.name}</h4>
          <div class="kcal">${meal.kcal} kcal</div>
          <div class="macro-row">
            <div class="macro-item"><div class="mval" style="color:#FF6B35;">${meal.macro.c}</div><div class="mlabel">탄수화물</div></div>
            <div class="macro-item"><div class="mval" style="color:#34A853;">${meal.macro.p}</div><div class="mlabel">단백질</div></div>
            <div class="macro-item"><div class="mval" style="color:#4285F4;">${meal.macro.f}</div><div class="mlabel">지방</div></div>
          </div>
        </div>
      </div>`;
  } else {
    html+=`<div style="background:#fff;border-radius:18px;padding:24px;text-align:center;margin-bottom:12px;border:1px solid #eee;"><div style="font-size:36px;opacity:0.25;margin-bottom:8px;">🍽️</div><div style="font-size:12px;color:#ccc;">식사 기록이 없는 날이에요</div></div>`;
  }

  html+=`
    <div class="mood-card">
      <h4>오늘 기분</h4>
      <div class="mood-options">
        ${[['😊','좋음'],['😐','보통'],['😴','피곤'],['💪','파이팅']].map(([e,l])=>`
          <div class="mood-btn ${meal&&meal.mood===e?'active':''}" onclick="document.querySelectorAll('.mood-btn').forEach(b=>b.classList.remove('active'));this.classList.add('active');">
            <div class="memoji">${e}</div><div class="mlabel">${l}</div>
          </div>`).join('')}
      </div>
    </div>
    <div class="day-diary-card">
      <h4>오늘의 일기 ✏️</h4>
      ${meal&&meal.diary
        ? `<div class="diary-text" id="diaryText_${day}">${meal.diary}</div>`
        : `<textarea class="diary-textarea" id="diaryTextarea_${day}" placeholder="오늘 식단 어땠나요? 몸 상태, 기분, 다짐을 자유롭게 적어보세요..."></textarea>
           <button class="save-diary-btn" onclick="saveDayDiary(${day})">저장하기</button>`
      }
    </div>`;

  document.getElementById('dayDetailContent').innerHTML=html;
  hideAll();
  showScreen('tab-day-detail');
  headerTitle.innerText=`4월 ${day}일`;
  backBtn.style.visibility='visible';
  backBtn.onclick=()=>{
    hideAll(); showScreen('tab-monthly-diary');
    headerTitle.innerText='다이어리'; backBtn.style.visibility='hidden';
    backBtn.onclick=null;
  };
}

function saveDayDiary(day) {
  const ta=document.getElementById(`diaryTextarea_${day}`);
  if(!ta||!ta.value.trim()) return alert('내용을 입력해주세요!');
  if(!MEALS[day]) MEALS[day]={emoji:'📝',name:'직접 입력',kcal:0,score:0,macro:{c:'-',p:'-',f:'-'}};
  MEALS[day].diary=ta.value.trim();
  DIARY_DAYS.add(day);
  alert('저장되었습니다!');
  initCalendar();
}
</script>
</body>
</html>
