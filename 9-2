const sulla = require("sulla");

sulla.create().then((client) => start(client));
var names = ["پیروزمندان"];
var allnames = [
  "ادراکی",
  "اسمعیل زاده",
  "باعزت",
  "پریشن",
  "تقوی",
  "پیروزمندان",
  "حیدری",
  "خوشرنگ",
  "دباغ منش",
  "رزمی",
  "رموئی",
  "روا",
  "رولدار",
  "شجاعی",
  "شریفی",
  "شقاقیان",
  "فرخنده",
  "قدیمی",
  "کاظمی فر",
  "کریمی",
  "محبی",
  "مرادی",
  "ممتازی",
  "میرزائی",
  "یزدانی",
];
let nallnames = trimArray(allnames);

function trimArray(wordlist) {
  for (var i = 0; i < wordlist.length; i++) {
    wordlist[i] = wordlist[i].split(" ").join("");
  }
  return wordlist;
}

function trimArr(wordlist) {
  for (var i = 0; i < wordlist.length; i++) {
    wordlist[i] = wordlist[i].split(" ").join("");
  }
  return wordlist;
}
let nnames = trimArr(names);

function start(client) {
  client.onStateChange((state) => {
    console.log(state);
    const conflits = [
      sulla.SocketState.CONFLICT,
      sulla.SocketState.UNPAIRED,
      sulla.SocketState.UNLAUNCHED,
    ];
    if (conflits.includes(state)) {
      client.useHere();
    }
  });
  client.onMessage((message) => {
    msg = message.body.split(" ").join("");
    if (nallnames.includes(msg)) {
      names.push(message.body.split(" ").join(""));
      client.sendText(message.from, message.body + " ثبت شد ✔️");
    } else if (message.body === "شروع") {
      client.sendText(
        message.from,
        "🕐حضور و غیاب کلاس از این لحظه آغاز شد \n  تنها  نام خانوادگی خود را به صورت کامل وارد کنید و منتظر پیام تایید باشید.\n توجه داشته باشید که نام و نام خانوادگی شما همانند دفتر کلاسی ذخیره شده است"
      );
    } else if (message.body === "پایان") {
      client.sendText(
        message.from,
        "زمان حضور و غیاب به پایان رسید . از این لحظه هیچ نام جدیدی در لیست ثبت نخواهد شد از فرستادن پیام خودداری کنید.🕥"
      );
    } else if (message.body === "نمایش لیست حاضران" || message.body === "1") {
      for (i = 0; i < names.length; i++) {
        client.sendText(message.from, names[i]);
      }
    } else if (message.body === "نمایش لیست غائبین" || message.body === "2") {
      let intersection = nnames.filter((x) => nallnames.includes(x));
      let difference = nnames
        .filter((x) => !nallnames.includes(x))
        .concat(nallnames.filter((x) => !nnames.includes(x)));
      client.sendText(message.from, "🔹🔹 لیست غائبین این زنگ 🔹🔹\n");
      for (l = 0; l < difference.length; l++) {
        let diff = difference[l];
        client.sendText(message.from, diff);
      }
    } else if (message.body === "مدیریت") {
      client.sendText(
        message.from,
        "به پنل مدیریت خوش آمدید.\n دستور ها: \n 1- نمایش لیست حاضران \n 2- نمایش لیست غائبین \n 3- ریست لیست حاضران \n - جهت استفاده از هر یک از دستورات می توانید شماره دستور - عدد انگلیسی باید باشد - و یا متن دستور را وارد نمایید"
      );
    } else if (message.body === "ریست لیست حاضران" || message.body === "3") {
      client.sendText(message.from, "تمامی حاضران از لیست پاک شدند.");
      names = [""];
    } else if (message.body === "راهنما") {
      client.sendText(
        message.from,
        "راهنما سامانه حضور و غیاب \n این سامانه از دو بخش دانش اموزان و مدیریت تشکیل شده است . دانش آموزان با وارد کردن کلمه حاضر، اطلاعات لازم از آنها خواسته می شود که سوالاتی که پس از این کلمه نمایش داده خواهند شد قابل افزایش و یا تنظیم مجدد می باشند . برای ورود به مدیریت و مشاهده آمار ها کلمه ی مدیریت باید ارسال شود و پس از آن پنل مدیریت نمایش داده می شود .\n تهیه شده توسط سینا پیروزمندان "
      );
      names = [""];
    }
  });
}
// sulla.create().then((name) => start(name));

// function start(name) {
//   name.onMessage((message) => {

//     client.sendText(message.from, names);

//   });
// }
