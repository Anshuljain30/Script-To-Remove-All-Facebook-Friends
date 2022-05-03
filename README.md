# Script-To-Remove-All-Facebook-Friends

// Open https://m.facebook.com/{{YOUR USER ID}}/friends in google chrome desktop
var incrementScroll = function () {
  window.scrollTo(0, document.body.scrollHeight);
};

// Please wait till all the friends are loaded
let myIntervalID = setInterval(incrementScroll, 1000);

// Once all friends are loaded, you can run this.
clearInterval(myIntervalID);

// Load friend Data
let myFriendsData = document.getElementsByClassName("_5d0x right");

// Parse Data
let friendsParsedData = [];
for (let eachFriend of myFriendsData) {
  friendsParsedData.push(JSON.parse(eachFriend.dataset.store));
}

// Get ID's of friends
let friendsIDs = [];

for (let eachFriend of friendsParsedData) {
  friendsIDs.push(eachFriend.id);
}

// Set a count variable and log variable
let myCount = 22;
myLog = [];

//start the script
for (let id of friendsIDs) {
  myCount = myCount + 2;
  myLog.push(
    await fetch("https://m.facebook.com/a/friends/remove/", {
      headers: {
        accept: "*/*",
        "accept-language": "en",
        "content-type": "application/x-www-form-urlencoded",
        "sec-ch-ua":
          '" Not A;Brand";v="99", "Chromium";v="100", "Google Chrome";v="100"',
        "sec-ch-ua-mobile": "?0",
        "sec-ch-ua-platform": '"macOS"',
        "sec-fetch-dest": "empty",
        "sec-fetch-mode": "cors",
        "sec-fetch-site": "same-origin",
        "x-fb-lsd": "XRhNVn5hDc-ojs9rWln0wL",
        "x-requested-with": "XMLHttpRequest",
        "x-response-format": "JSONStream",
      },
      referrer: "https://m.facebook.com/mnvrjn/friends",
      referrerPolicy: "origin-when-cross-origin",
      body: `friend_id=${id}&noReload=true&unref=bd_friends_tab&fb_dtsg=AQGCHBHQwYywOVM%3A15%3A1650868172&jazoest=22007&lsd=XRhNVn5hDc-ojs9rWln0wL&__dyn=1KQEGiFo525Ujwh8-t0BBBgS5UqxK12wAxu3-U2owSwMxW0Horx64o1j8hwem0iy1gCwjE1xoswaq1Jwt8-0nSUS0na1gwwyo36w9yq3q0H8-7E2swp834wmE2ewnE2Lx-220n6azo11E2ZwrU&__csr=&__req=${myCount}&__a=AYmAn8KauD_pfh5ScRljaPWx8asoV81awvJfIP7BTzUmWu37OBEOU-jzmuK_9Q670HiJrqxts8DKv6aB8eW1rKpdh0f4Q7vrXpfQuEXATmrd0g&__user=100005759112700`,
      method: "POST",
      mode: "cors",
      credentials: "include",
    })
  );
}
