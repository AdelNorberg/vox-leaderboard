<template>
  <div class="cont">
    <div v-if="!isMobile" class="leaderboard">
      <div class="header">CLAN WAR</div>
      <div class="not-official">Not official Voxiom.io leaderboard</div>

      <div class="description">
        The rating is based on the sum of all members levels
      </div>

      <div class="last-upd">Latest leaderboard update: 08.01.2023</div>

      <div class="list">
        <div v-for="(clan, key) in allClans" :key="key" class="clan">
          <div class="place">{{ key + 1 }}</div>
          <div class="tag">{{ clan.tag }}</div>
          <div class="name">{{ clan.name }}</div>
          <div class="leader">{{ clan.leader }}</div>
          <div class="count">{{ clan.count }}</div>
          <div class="all-levels">{{ clan.allLevels }}</div>
        </div>
      </div>

      <img :src="bgSvg" class="img-1" />
      <img :src="bg2Svg" class="img-2" />
      <img :src="bg3Svg" class="img-3" />
    </div>

    <div v-else class="is-mobile">MOBILE OR TABLET NOT SUPPORTED. SORRY!</div>
  </div>
</template>

<style lang="scss">
@import "normalize.css";
@import url("https://fonts.googleapis.com/css2?family=Kanit:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

body,
#app {
  width: 100vw;
  height: 100vh;
  padding: 0;
  margin: 0;
  font-family: "Kanit", sans-serif;
  font-weight: 500;
}

html {
  font-size: 16px;

  @media (max-width: 1800px) {
    font-size: 14px;
  }

  @media (max-width: 1600px) {
    font-size: 13px;
  }

  @media (max-width: 1200px) {
    font-size: 12px;
  }

  @media (max-width: 1100px) {
    font-size: 12px;
  }

  @media (max-width: 900px) {
    font-size: 10px;
  }

  @media (max-width: 736px) {
    font-size: 9px;
  }

  @media (max-width: 667px) {
    font-size: 8px;
  }
}
</style>

<style lang="scss" scoped>
.leaderboard,
.cont {
  width: 100vw;
  height: 100vh;
  background: linear-gradient(97.27deg, #105fa8 5.99%, #009ef8 98.74%);
  color: white;
  position: relative;
}

.is-mobile {
  width: 100vw;
  height: 100vh;
  background: linear-gradient(97.27deg, #105fa8 5.99%, #009ef8 98.74%);
  color: white;
  position: relative;
  font-size: 3.5rem;
  text-align: center;
  padding-top: 40vh;
  box-sizing: border-box;
}

.header {
  text-shadow: 0px 0.313rem 0.313rem rgba(0, 0, 0, 0.25);
  font-size: 5.25rem;
  font-weight: Bold;
  width: 100%;
  text-align: center;
  padding-top: 3.125rem;
  position: relative;
  z-index: 5;
}

.not-official {
  color: rgba(255, 218, 72, 1);
  position: absolute;
  top: 0;
  left: 0;
  font-size: 1.5rem;
  padding: 1.25rem 0 0 1.25rem;
}

.img-1 {
  position: absolute;
  right: 0;
  bottom: 0;
  z-index: 1;
  width: 30rem;
  height: 62.5rem;
}

.img-2 {
  position: absolute;
  left: 18.75rem;
  top: 9.375rem;
  width: 80.25rem;
  height: 4.375rem;
}

.img-3 {
  position: absolute;
  right: 0;
  bottom: 0;
  z-index: 0;
  width: 77.25rem;
  height: 67.813rem;
}

.description {
  font-size: 1.938rem;
  font-weight: Bold;
  text-shadow: 0px 0.188rem 0.188rem rgba(0, 0, 0, 0.25);
  text-align: center;
  position: relative;
  z-index: 2;
  margin-top: 1.25rem;
}

.list {
  width: 87.5rem;
  height: 45rem;
  display: flex;
  flex-wrap: wrap;
  background-color: #0e5a9a;
  position: absolute;
  bottom: 0;
  left: 0;
  overflow-y: auto;
  z-index: 2;

  &::-webkit-scrollbar {
    width: 0.5rem;
    background: rgba(7, 24, 53, 0.5);
  }

  &::-webkit-scrollbar-thumb {
    background: rgba(98, 124, 168, 0.8);
    border-radius: 0.25rem;
  }
}

.clan {
  display: flex;
  width: 39rem;
  margin-left: 1.25rem;
  background-color: #0e66b1;
  margin-top: 0.625rem;
  height: 2.438rem;
  align-items: center;
  padding: 0 1.25rem;
}

.tag {
  width: 5rem;
  text-align: left;
}

.place {
  text-shadow: 0px 2px 2px rgba(0, 0, 0, 0.25);
  font-size: 1.5rem;
  color: rgba(255, 218, 72, 1);
  width: 3rem;
}

.name {
  width: 10rem;
}

.leader {
  width: 14rem;
}

.count {
  width: 2rem;
}

.all-levels {
  width: 5rem;
  padding-left: 2rem;
}

.last-upd {
  position: absolute;
  left: 1.5rem;
  font-size: 1.5rem;
  bottom: 45.5rem;
}
</style>

<script setup>
import "@/assets/global.scss?inline";
import bgSvg from "@/assets/bg.svg";
import bg2Svg from "@/assets/bg2.svg";
import bg3Svg from "@/assets/bg3.svg";
import UAParser from "ua-parser-js";
import { ref, onMounted } from "vue";

const isMobile = ref(false);

onMounted(async () => {
  try {
    const uaparser = await new UAParser();
    const deviceType = uaparser.getDevice().type;
    if (deviceType === "mobile" || deviceType === "tablet")
      isMobile.value = true;
  } catch (e) {
    console.error(e);
  }
});

const allClans = [
  {
    leader: "Nm_HellBoy_",
    count: 49,
    tag: "Nm",
    name: "No Mercy",
    scores: 0,
    allLevels: 4611,
  },
  {
    leader: "ISO_theReaper",
    count: 48,
    tag: "ISO",
    name: "IsoNation",
    scores: 0,
    allLevels: 4597,
  },
  {
    leader: "Sucker_Fr",
    count: 49,
    tag: "BEST",
    name: "Euro skilled team",
    scores: 0,
    allLevels: 4460,
  },
  {
    leader: "RTvzy",
    count: 50,
    tag: "Ns",
    name: "No Surprises",
    scores: 0,
    allLevels: 2990,
  },
  {
    leader: "SWATOXIC",
    count: 48,
    tag: "SWAT",
    name: "SWATTOXIC",
    scores: 0,
    allLevels: 2956,
  },
  {
    leader: "23_pro",
    count: 44,
    tag: "EzPz",
    name: "ALL Pros",
    scores: 0,
    allLevels: 2846,
  },
  {
    leader: "Levo_Huntz",
    count: 50,
    tag: "I8",
    name: "RED INFINITY",
    scores: 0,
    allLevels: 2599,
  },
  {
    leader: "IR_Taha2006",
    count: 30,
    tag: "Pro",
    name: "Voxiom Hunters",
    scores: 0,
    allLevels: 2576,
  },
  {
    leader: "Sbeve",
    count: 33,
    tag: "Or",
    name: "The Order",
    scores: 0,
    allLevels: 2514,
  },
  {
    leader: "pandas_tab",
    count: 47,
    tag: "TP",
    name: "The Pandas",
    scores: 0,
    allLevels: 2390,
  },
  {
    leader: "PH_TimeLezZ",
    count: 49,
    tag: "PH",
    name: "PH Armed Forces",
    scores: 0,
    allLevels: 2380,
  },
  {
    leader: "JP_Ryotaro",
    count: 47,
    tag: "ND",
    name: "NADA",
    scores: 0,
    allLevels: 2371,
  },
  {
    leader: "LifeIs-a-stan-0966",
    count: 47,
    tag: "SMG",
    name: "I8 Sub Machine",
    scores: 0,
    allLevels: 2332,
  },
  {
    leader: "TC_Dang_Thi_KhLinh",
    count: 39,
    tag: "TC",
    name: "VIET NAM",
    scores: 0,
    allLevels: 2202,
  },
  {
    leader: "Numbers",
    count: 38,
    tag: "OvO",
    name: "The Sandpipers",
    scores: 0,
    allLevels: 2157,
  },
  {
    leader: "Envious",
    count: 45,
    tag: "nU",
    name: "Envious",
    scores: 0,
    allLevels: 2061,
  },
  {
    leader: "X_LSPD_X",
    count: 50,
    tag: "LSPD",
    name: "SWAT",
    scores: 0,
    allLevels: 2055,
  },
  {
    leader: "HARSKWARRIOR_2",
    count: 50,
    tag: "Opt",
    name: "Over  Powered Team",
    scores: 0,
    allLevels: 2037,
  },
  {
    leader: "ISO_Nation",
    count: 44,
    tag: "IISO",
    name: "IsoNation II",
    scores: 0,
    allLevels: 2007,
  },
  {
    leader: "LTD_BlackMoon_VN",
    count: 43,
    tag: "LTD",
    name: "Legendary Resurre",
    scores: 0,
    allLevels: 1920,
  },
  {
    leader: "NamelessCorpse",
    count: 42,
    tag: "PYK",
    name: "Psycho Killers",
    scores: 0,
    allLevels: 1858,
  },
  {
    leader: "Crazy-Killer-Bunny",
    count: 34,
    tag: "Fire",
    name: "Deadly Dragons",
    scores: 0,
    allLevels: 1846,
  },
  {
    leader: "TheMagicProYT",
    count: 47,
    tag: "TSL",
    name: "The Space Legends",
    scores: 0,
    allLevels: 1841,
  },
  {
    leader: "TE_BaoChat_",
    count: 39,
    tag: "the",
    name: "vietnamvaoday",
    scores: 0,
    allLevels: 1780,
  },
  {
    leader: "HellBoy2024",
    count: 27,
    tag: "XNmX",
    name: "No Mercy-X",
    scores: 0,
    allLevels: 1758,
  },
  {
    leader: "Desean_",
    count: 48,
    tag: "OSS",
    name: "One Shot Squad",
    scores: 0,
    allLevels: 1739,
  },
  {
    leader: "Wolf_22",
    count: 50,
    tag: "WOLF",
    name: "Clan of the Wolves",
    scores: 0,
    allLevels: 1717,
  },
  {
    leader: "Autumn_Leaf",
    count: 49,
    tag: "MF",
    name: "Mythical Force",
    scores: 0,
    allLevels: 1670,
  },
  {
    leader: "clown_pierce",
    count: 49,
    tag: "UWU",
    name: "the UWU gang",
    scores: 0,
    allLevels: 1670,
  },
  {
    leader: "KingNkt12",
    count: 48,
    tag: "VUA",
    name: "Kings of  VietNam",
    scores: 0,
    allLevels: 1637,
  },
  {
    leader: "Aaryankiller",
    count: 50,
    tag: "Hind",
    name: "Indian Clan",
    scores: 0,
    allLevels: 1632,
  },
  {
    leader: "orzubek2009YT",
    count: 50,
    tag: "UAF",
    name: "Usa  Armed Forces",
    scores: 0,
    allLevels: 1627,
  },
  {
    leader: "Sulhi_speedrun",
    count: 50,
    tag: "gg",
    name: "Technoblade gg",
    scores: 0,
    allLevels: 1612,
  },
  {
    leader: "osas",
    count: 50,
    tag: "GEO",
    name: "GEORGIAN FORCES",
    scores: 0,
    allLevels: 1601,
  },
  {
    leader: "c3_pro",
    count: 49,
    tag: "PR0",
    name: "PROS",
    scores: 0,
    allLevels: 1600,
  },
  {
    leader: "Creeper-Awman",
    count: 48,
    tag: "Lol",
    name: "ABigClumpOfCreep",
    scores: 0,
    allLevels: 1591,
  },
  {
    leader: "FG_Junichiro_God",
    count: 47,
    tag: "FG",
    name: "Flaming_Gods",
    scores: 0,
    allLevels: 1584,
  },
  {
    leader: "supermike",
    count: 50,
    tag: "MIKE",
    name: "SUPERCLAN",
    scores: 0,
    allLevels: 1577,
  },
  {
    leader: "RI8_VentrIX",
    count: 50,
    tag: "RI8",
    name: "RED INFINITY III",
    scores: 0,
    allLevels: 1567,
  },
  {
    leader: "PiwPiw",
    count: 41,
    tag: "BOLT",
    name: "TEMPEST",
    scores: 0,
    allLevels: 1566,
  },
  {
    leader: "VRGV_Xenon_BG",
    count: 24,
    tag: "VRGV",
    name: "VRGV Envertion VN",
    scores: 0,
    allLevels: 1564,
  },
  {
    leader: "JudahPlayzGamingYT",
    count: 50,
    tag: "End",
    name: "The Enderian",
    scores: 0,
    allLevels: 1561,
  },
  {
    leader: "Britania",
    count: 49,
    tag: "OOH",
    name: "NATO  and OON",
    scores: 0,
    allLevels: 1517,
  },
  {
    leader: "d9g0_YT",
    count: 40,
    tag: "DG",
    name: "drak night",
    scores: 0,
    allLevels: 1512,
  },
  {
    leader: "--beluga--",
    count: 50,
    tag: "CatS",
    name: "Cats Fan",
    scores: 0,
    allLevels: 1510,
  },
  {
    leader: "queen_13",
    count: 50,
    tag: "FRDS",
    name: "F R I E N D S",
    scores: 0,
    allLevels: 1481,
  },
  {
    leader: "MUS_ALLAH_SOLDIER",
    count: 37,
    tag: "MUS",
    name: "MUSLIM ARMY",
    scores: 0,
    allLevels: 1471,
  },
  {
    leader: "NPC_Laroi",
    count: 50,
    tag: "NPC",
    name: "VietNamTheBest",
    scores: 0,
    allLevels: 1462,
  },
  {
    leader: "TEAM_MARYPLAYZ",
    count: 50,
    tag: "TEAM",
    name: "TEAMWORK GROUP",
    scores: 0,
    allLevels: 1448,
  },
  {
    leader: "pandasayshewo",
    count: 48,
    tag: "PNDA",
    name: "Panda palace",
    scores: 0,
    allLevels: 1439,
  },
  {
    leader: "Voxy-10",
    count: 50,
    tag: "EZ",
    name: "ELECTRO WIZARDS",
    scores: 0,
    allLevels: 1438,
  },
  {
    leader: "mandogxpro",
    count: 50,
    tag: "lets",
    name: "proesports",
    scores: 0,
    allLevels: 1419,
  },
  {
    leader: "JimmyNewtron",
    count: 50,
    tag: "BBs",
    name: "Bacon Boys",
    scores: 0,
    allLevels: 1382,
  },
  {
    leader: "OffLight",
    count: 49,
    tag: "WISM",
    name: "Smash Win",
    scores: 0,
    allLevels: 1379,
  },
  {
    leader: "Dragon_Strom",
    count: 49,
    tag: "drag",
    name: "Dragon_Army",
    scores: 0,
    allLevels: 1376,
  },
  {
    leader: "Gonzalezo",
    count: 49,
    tag: "RD",
    name: "Reyes dragon",
    scores: 0,
    allLevels: 1370,
  },
  {
    leader: "NGName",
    count: 43,
    tag: "NG",
    name: "NOT GG",
    scores: 0,
    allLevels: 1369,
  },
  {
    leader: "AR972",
    count: 41,
    tag: "HW",
    name: "Hunting Wolves",
    scores: 0,
    allLevels: 1364,
  },
  {
    leader: "Agony_Echo_",
    count: 50,
    tag: "Echo",
    name: "The Echo",
    scores: 0,
    allLevels: 1358,
  },
  {
    leader: "TTop1_DATNEKKK",
    count: 50,
    tag: "DEST",
    name: "DESTROY",
    scores: 0,
    allLevels: 1347,
  },
  {
    leader: "James-Vago",
    count: 50,
    tag: "Sup",
    name: "World Domination",
    scores: 0,
    allLevels: 1344,
  },
  {
    leader: "H4rr4Z128",
    count: 33,
    tag: "asia",
    name: "Malaysia paskal",
    scores: 0,
    allLevels: 1333,
  },
  {
    leader: "Cactus_eater",
    count: 13,
    tag: "SG",
    name: "Sweaty_Grinders",
    scores: 0,
    allLevels: 1330,
  },
  {
    leader: "Dragold_plays_yt",
    count: 44,
    tag: "Bruh",
    name: "The legends",
    scores: 0,
    allLevels: 1328,
  },
  {
    leader: "FRNTL_YUYU64",
    count: 50,
    tag: "AYRU",
    name: "oiii",
    scores: 0,
    allLevels: 1319,
  },
  {
    leader: "MachineDragon",
    count: 48,
    tag: "nu7",
    name: "MTF Nu-7HammerDown",
    scores: 0,
    allLevels: 1316,
  },
  {
    leader: "Arson-is-fun",
    count: 50,
    tag: "7th",
    name: "7th Heaven",
    scores: 0,
    allLevels: 1310,
  },
  {
    leader: "CommunistVietnam",
    count: 50,
    tag: "USSR",
    name: "The_Soviet_Union",
    scores: 0,
    allLevels: 1305,
  },
  {
    leader: "killyou",
    count: 50,
    tag: "TKAS",
    name: "The killyou Clan",
    scores: 0,
    allLevels: 1303,
  },
  {
    leader: "tiger61525",
    count: 50,
    tag: "TG",
    name: "TIGER",
    scores: 0,
    allLevels: 1279,
  },
  {
    leader: "75289821",
    count: 50,
    tag: "VL",
    name: "ETERNITY WARRIORS",
    scores: 0,
    allLevels: 1276,
  },
  {
    leader: "-anonymous-",
    count: 43,
    tag: "TXL",
    name: "The Xylofiles",
    scores: 0,
    allLevels: 1275,
  },
  {
    leader: "Pro-Sniper",
    count: 49,
    tag: "Boss",
    name: "Sniper",
    scores: 0,
    allLevels: 1258,
  },
  {
    leader: "MrClown",
    count: 40,
    tag: "STF",
    name: "Special Task Force",
    scores: 0,
    allLevels: 1251,
  },
  {
    leader: "LXFD_Andrey-Nayaka",
    count: 43,
    tag: "LXFD",
    name: "LXFD basement clan",
    scores: 0,
    allLevels: 1229,
  },
  {
    leader: "takesuraimu_2843",
    count: 48,
    tag: "GT",
    name: "Gran Turismo",
    scores: 0,
    allLevels: 1228,
  },
  {
    leader: "Ucconspy",
    count: 41,
    tag: "STAR",
    name: "GodsFavouriteStar",
    scores: 0,
    allLevels: 1203,
  },
  {
    leader: "DADADA",
    count: 32,
    tag: "CRIB",
    name: "XX_Crib_XX",
    scores: 0,
    allLevels: 1197,
  },
  {
    leader: "xXLegendXx",
    count: 44,
    tag: "ZH",
    name: "Zeno Hunterz",
    scores: 0,
    allLevels: 1173,
  },
  {
    leader: "Arifdaking",
    count: 48,
    tag: "WW3",
    name: "Undefeated Warrior",
    scores: 0,
    allLevels: 1163,
  },
  {
    leader: "navyassasan1234",
    count: 50,
    tag: "ioe",
    name: "lockout",
    scores: 0,
    allLevels: 1160,
  },
  {
    leader: "Naho",
    count: 48,
    tag: "CT",
    name: "Chemical Thug",
    scores: 0,
    allLevels: 1153,
  },
  {
    leader: "Hell-Fire",
    count: 23,
    tag: "IMP",
    name: "I-M-P",
    scores: 0,
    allLevels: 1147,
  },
  {
    leader: "Bearrr",
    count: 16,
    tag: "DYA",
    name: "Dynasty Animals",
    scores: 0,
    allLevels: 1131,
  },
  {
    leader: "Demon-Assassin",
    count: 32,
    tag: "SAS",
    name: "-Sniper_Assassins-",
    scores: 0,
    allLevels: 1125,
  },
  {
    leader: "LZB_Kaito",
    count: 13,
    tag: "LZB",
    name: "Lazy Boy",
    scores: 0,
    allLevels: 1125,
  },
  {
    leader: "Sealteam2",
    count: 50,
    tag: "AK47",
    name: "AK-47",
    scores: 0,
    allLevels: 1124,
  },
  {
    leader: "RestiaAshdoll",
    count: 49,
    tag: "ASTW",
    name: "AnimeSTierWaifu",
    scores: 0,
    allLevels: 1116,
  },
  {
    leader: "VillanYT",
    count: 48,
    tag: "ViLn",
    name: "Villan Army",
    scores: 0,
    allLevels: 1114,
  },
  {
    leader: "Ace_Crusader",
    count: 24,
    tag: "POG",
    name: "Crusaders",
    scores: 0,
    allLevels: 1099,
  },
  {
    leader: "RI-YKSOH",
    count: 35,
    tag: "RI",
    name: "RI TEAM",
    scores: 0,
    allLevels: 1096,
  },
  {
    leader: "DF_LALAL_VN",
    count: 40,
    tag: "DF",
    name: "Dream in Future",
    scores: 0,
    allLevels: 1088,
  },
  {
    leader: "THARUN_321",
    count: 38,
    tag: "LGS",
    name: "LEGENDARY_WARRIORS",
    scores: 0,
    allLevels: 1082,
  },
  {
    leader: "_Ay_leader_",
    count: 31,
    tag: "CLIX",
    name: "C L I X",
    scores: 0,
    allLevels: 1065,
  },
  {
    leader: "XavoS_XD",
    count: 30,
    tag: "xo",
    name: "Xeno",
    scores: 0,
    allLevels: 1062,
  },
  {
    leader: "NikiDaProGamer",
    count: 37,
    tag: "GOD",
    name: "Gamer Gods",
    scores: 0,
    allLevels: 1058,
  },
  {
    leader: "COMMANDERJIMMY",
    count: 42,
    tag: "FHF",
    name: "Free hispanic Forc",
    scores: 0,
    allLevels: 1053,
  },
  {
    leader: "shadosking",
    count: 25,
    tag: "tsk",
    name: "the shadow killer",
    scores: 0,
    allLevels: 1051,
  },
  {
    leader: "ahmet-kaan",
    count: 40,
    tag: "OTO",
    name: "Ottomon Empire",
    scores: 0,
    allLevels: 1046,
  },
  {
    leader: "FAZLILBULLETMAN",
    count: 40,
    tag: "FAZ",
    name: "FAZ",
    scores: 0,
    allLevels: 1039,
  },
];
</script>
