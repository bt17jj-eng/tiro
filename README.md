# import requests,re,json,os
R="\033[91m";G="\033[92m";Y="\033[93m";C="\033[96m";B="\033[94m";P="\033[95m";X="\033[0m"

# ============================================
# 🧑‍💻 معلومات صانع الأداة
# ============================================
CREATOR = {
    "username": "user_dedsec",
    "nickname": "DEDSEC",
    "bio": "⌨️ Cybersecurity | Python Developer | OSINT",
    "link": "https://www.tiktok.com/@user_dedsec"
}

# ============================================
# 🌍 قائمة اللغات (20 لغة)
# ============================================
LANGUAGES = {
    "1": {"name": "العربية", "code": "ar"},
    "2": {"name": "English", "code": "en"},
    "3": {"name": "Français", "code": "fr"},
    "4": {"name": "Español", "code": "es"},
    "5": {"name": "Deutsch", "code": "de"},
    "6": {"name": "Italiano", "code": "it"},
    "7": {"name": "Português", "code": "pt"},
    "8": {"name": "Русский", "code": "ru"},
    "9": {"name": "日本語", "code": "ja"},
    "10": {"name": "한국어", "code": "ko"},
    "11": {"name": "中文", "code": "zh"},
    "12": {"name": "हिन्दी", "code": "hi"},
    "13": {"name": "Türkçe", "code": "tr"},
    "14": {"name": "Nederlands", "code": "nl"},
    "15": {"name": "Polski", "code": "pl"},
    "16": {"name": "Svenska", "code": "sv"},
    "17": {"name": "Dansk", "code": "da"},
    "18": {"name": "Suomi", "code": "fi"},
    "19": {"name": "Ελληνικά", "code": "el"},
    "20": {"name": "Čeština", "code": "cs"}
}

# ============================================
# 📝 قاموس الترجمات (مختصر للعربية والإنجليزية فقط عشان الكود ما يطول)
# باقي اللغات نفس الكود السابق
# ============================================
def get_texts(lang_code):
    texts = {
        "ar": {
            "title": "💀 TikTok OSINT 💀",
            "enter_user": "ادخل يوزر (q للخروج): ",
            "searching": "⏳ جاري البحث...",
            "not_found": "❌ الحساب غير موجود!",
            "exit": "🚪 خروج...",
            "username": "المستخدم",
            "nickname": "اللقب",
            "id": "المعرف",
            "status": "الحالة",
            "public": "عام",
            "private": "خاص",
            "verified": "موثق",
            "yes": "نعم",
            "no": "لا",
            "stats": "الاحصائيات",
            "followers": "متابعون",
            "following": "يتابع",
            "likes": "اعجابات",
            "videos": "فيديوهات",
            "bio": "البيو",
            "bio_link": "رابط البيو",
            "avatar": "صورة البروفايل",
            "sec_uid": "Sec UID",
            "press_enter": "اضغط Enter للمتابعة...",
            "creator": "🧑‍💻 صانع الأداة",
            "follow_him": "📱 تابعني على تيك توك"
        },
        "en": {
            "title": "💀 TikTok OSINT 💀",
            "enter_user": "Enter username (q to quit): ",
            "searching": "⏳ Searching...",
            "not_found": "❌ User not found!",
            "exit": "🚪 Exiting...",
            "username": "Username",
            "nickname": "Nickname",
            "id": "ID",
            "status": "Status",
            "public": "Public",
            "private": "Private",
            "verified": "Verified",
            "yes": "Yes",
            "no": "No",
            "stats": "Statistics",
            "followers": "Followers",
            "following": "Following",
            "likes": "Likes",
            "videos": "Videos",
            "bio": "Bio",
            "bio_link": "Bio Link",
            "avatar": "Profile Picture",
            "sec_uid": "Sec UID",
            "press_enter": "Press Enter to continue...",
            "creator": "🧑‍💻 Tool Creator",
            "follow_him": "📱 Follow me on TikTok"
        }
    }
    # إذا كانت اللغة غير العربية أو الإنجليزية، استخدم الإنجليزية
    return texts.get(lang_code, texts["en"])

def clear():os.system('cls' if os.name=='nt' else 'clear')

def select_language():
    clear()
    print(R + "\n   █████╗  ██████╗ ███████╗██╗███╗   ██╗████████╗\n  ██╔══██╗██╔═══██╗██╔════╝██║████╗  ██║╚══██╔══╝\n  ███████║██║   ██║███████╗██║██╔██╗ ██║   ██║   \n  ██╔══██║██║   ██║╚════██║██║██║╚██╗██║   ██║   \n  ██║  ██║╚██████╔╝███████║██║██║ ╚████║   ██║   \n  ╚═╝  ╚═╝ ╚═════╝ ╚══════╝╚═╝╚═╝  ╚═══╝   ╚═╝   \033[0m")
    print(Y + "\n🌍 اختر لغتك / Choose your language:\n" + X)
    for key, lang in LANGUAGES.items():
        print(f"{G}{key}{X}. {lang['name']}")
    print("\n" + Y + "➜ " + X)
    choice = input().strip()
    while choice not in LANGUAGES:
        print(R + "❌ اختيار غير صحيح! / Invalid choice!" + X)
        choice = input(Y + "➜ " + X).strip()
    return LANGUAGES[choice]["code"]

def show_creator(t):
    print(f"""
{P}╔═══════════════════════════════════════╗
║         {t['creator']}         ║
╠═══════════════════════════════════════╣
║ {C}👤 {CREATOR['username']}{X}
║ {G}📛 {CREATOR['nickname']}{X}
║ {Y}📝 {CREATOR['bio']}{X}
║ {B}🔗 {CREATOR['link']}{X}
╚═══════════════════════════════════════╝{X}
""")

def get_user(u):
    try:
        r=requests.get(f"https://www.tiktok.com/@{u}",headers={"User-Agent":"Mozilla/5.0 (iPhone; CPU iPhone OS 16_0 like Mac OS X) AppleWebKit/605.1.15"})
        if r.status_code!=200:return None
        m=re.search(r'<script id="__UNIVERSAL_DATA_FOR_REHYDRATION__" type="application/json">(.*?)</script>',r.text)
        if not m:m=re.search(r'<script id="SIGI_STATE" type="application/json">(.*?)</script>',r.text)
        if not m:return None
        d=json.loads(m.group(1))
        try:
            ud=d.get("__DEFAULT_SCOPE__",{}).get("webapp.user-detail",{}).get("userInfo",{})
            uu=ud.get("user",{});s=ud.get("stats",{})
        except:
            try:
                uu=d.get("UserModule",{}).get("users",{}).get(u,{})
                s=uu.get("stats",{})
            except:
                return None
        if not uu:return None
        return{
            "user":uu.get("uniqueId",u),
            "name":uu.get("nickname","N/A"),
            "id":uu.get("id","N/A"),
            "fol":s.get("followerCount",0),
            "fing":s.get("followingCount",0),
            "likes":s.get("heartCount",0),
            "vid":s.get("videoCount",0),
            "bio":uu.get("signature","N/A"),
            "ver":uu.get("verified",False),
            "priv":uu.get("privateAccount",False),
            "sec_uid":uu.get("secUid","N/A"),
            "bio_link":uu.get("bioLink",{}).get("link","N/A") if uu.get("bioLink") else "N/A",
            "avatar":uu.get("avatarMedium","N/A")
        }
    except:return None

def show(u, t):
    clear()
    print(R + "\n   █████╗  ██████╗ ███████╗██╗███╗   ██╗████████╗\n  ██╔══██╗██╔═══██╗██╔════╝██║████╗  ██║╚══██╔══╝\n  ███████║██║   ██║███████╗██║██╔██╗ ██║   ██║   \n  ██╔══██║██║   ██║╚════██║██║██║╚██╗██║   ██║   \n  ██║  ██║╚██████╔╝███████║██║██║ ╚████║   ██║   \n  ╚═╝  ╚═╝ ╚═════╝ ╚══════╝╚═╝╚═╝  ╚═══╝   ╚═╝   \033[0m")
    if not u:
        print(R + t["not_found"] + X)
        show_creator(t)
        return
    v = G + t["yes"] + X if u["ver"] else R + t["no"] + X
    p = G + t["public"] + X if not u["priv"] else R + t["private"] + X
    print(f"""{Y}{t['username']}: {X}{u['user']}
{G}{t['nickname']}: {X}{u['name']}
{C}{t['id']}: {X}{u['id']}
{G}{t['status']}: {X}{p}
{C}{t['verified']}: {X}{v}
{Y}{t['stats']}:{X}
 👥 {t['followers']}: {u['fol']:,}
 👣 {t['following']}: {u['fing']:,}
 ❤️ {t['likes']}: {u['likes']:,}
 🎬 {t['videos']}: {u['vid']:,}
{G}{t['bio']}: {X}{u['bio']}
{C}{t['bio_link']}: {X}{u['bio_link']}
{P}{t['avatar']}: {X}{u['avatar']}
{B}{t['sec_uid']}: {X}{u['sec_uid']}
""")
    show_creator(t)

def main():
    lang_code = select_language()
    t = get_texts(lang_code)
    while 1:
        clear()
        print(Y + f"\n{t['title']}\n" + X)
        u = input(G + t["enter_user"] + X).strip()
        if u.lower() == "q":
            print(R + t["exit"] + X)
            break
        if u:
            print(Y + t["searching"] + X)
            show(get_user(u), t)
        input("\n" + Y + t["press_enter"] + X)

if __name__ == "__main__":
    try:
        main()
    except KeyboardInterrupt:
        print(R + "\n⚠️ تم الإيقاف / Stopped" + X)
