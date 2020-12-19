<script>
  import liff from "@line/liff";

  window.onload = function (e) {
    liff.init({liffId: LIFF_ID},function (data) {
      initializeApp(data);
    });
  };

  function initializeApp(data) {
    document.getElementById("languagefield").textContent = data.language;
    document.getElementById("viewtypefield").textContent = data.context.viewType;
    document.getElementById("useridfield").textContent = data.context.userId;
    document.getElementById("utouidfield").textContent = data.context.utouId;
    document.getElementById("roomidfield").textContent = data.context.roomId;
    document.getElementById("groupidfield").textContent = data.context.groupId;

    // openWindow call
    document
      .getElementById("openwindowbutton")
      .addEventListener("click", function () {
        liff.openWindow({
          url: "https://line.me",
        });
      });

    // closeWindow call
    document
      .getElementById("closewindowbutton")
      .addEventListener("click", function () {
        liff.closeWindow();
      });

    // sendMessages call
    document
      .getElementById("sendmessagebutton")
      .addEventListener("click", function () {
        liff
          .sendMessages([
            {
              type: "text",
              text: "You've successfully sent a message! Hooray!",
            },
            {
              type: "sticker",
              packageId: "2",
              stickerId: "144",
            },
          ])
          .then(function () {
            window.alert("Message sent");
          })
          .catch(function (error) {
            window.alert("Error sending message: " + error);
          });
      });

    // get access token
    document
      .getElementById("getaccesstoken")
      .addEventListener("click", function () {
        const accessToken = liff.getAccessToken();
        document.getElementById("accesstokenfield").textContent = accessToken;
        toggleAccessToken();
      });

    // get profile call
    document
      .getElementById("getprofilebutton")
      .addEventListener("click", function () {
        liff
          .getProfile()
          .then(function (profile) {
            document.getElementById("useridprofilefield").textContent =
              profile.userId;
            document.getElementById("displaynamefield").textContent =
              profile.displayName;

            const profilePictureDiv = document.getElementById(
              "profilepicturediv"
            );
            if (profilePictureDiv.firstElementChild) {
              profilePictureDiv.removeChild(
                profilePictureDiv.firstElementChild
              );
            }
            const img = document.createElement("img");
            img.src = profile.pictureUrl;
            img.alt = "Profile Picture";
            profilePictureDiv.appendChild(img);

            document.getElementById("statusmessagefield").textContent =
              profile.statusMessage;
            toggleProfileData();
          })
          .catch(function (error) {
            window.alert("Error getting profile: " + error);
          });
      });
  }

  function toggleAccessToken() {
    toggleElement("accesstokendata");
  }

  function toggleProfileData() {
    toggleElement("profileinfo");
  }

  function toggleElement(elementId) {
    const elem = document.getElementById(elementId);
    if (elem.offsetWidth > 0 && elem.offsetHeight > 0) {
      elem.style.display = "none";
    } else {
      elem.style.display = "block";
    }
  }
</script>

<div class="buttongroup">
  <div class="buttonrow">
    <button id="openwindowbutton">Open Window</button>
    <button id="closewindowbutton">Close Window</button>
  </div>
  <div class="buttonrow">
    <button id="getaccesstoken">Get Access Token</button>
    <button id="getprofilebutton">Get Profile</button>
    <button id="sendmessagebutton">Send Message</button>
  </div>
</div>

<div id="accesstokendata">
  <h2>Access Token</h2>
  <a href="#" onclick="toggleAccessToken()">Close Access Token</a>
  <table border="1">
    <tr>
      <th>accessToken</th>
      <td id="accesstokenfield" />
    </tr>
  </table>
</div>

<div id="profileinfo">
  <h2>Profile</h2>
  <a href="#" onclick="toggleProfileData()">Close Profile</a>
  <div id="profilepicturediv" />
  <table border="1">
    <tr>
      <th>userId</th>
      <td id="useridprofilefield" />
    </tr>
    <tr>
      <th>displayName</th>
      <td id="displaynamefield" />
    </tr>
    <tr>
      <th>statusMessage</th>
      <td id="statusmessagefield" />
    </tr>
  </table>
</div>

<div id="liffdata">
  <h2>LIFF Data</h2>
  <table border="1">
    <tr>
      <th>language</th>
      <td id="languagefield" />
    </tr>
    <tr>
      <th>context.viewType</th>
      <td id="viewtypefield" />
    </tr>
    <tr>
      <th>context.userId</th>
      <td id="useridfield" />
    </tr>
    <tr>
      <th>context.utouId</th>
      <td id="utouidfield" />
    </tr>
    <tr>
      <th>context.roomId</th>
      <td id="roomidfield" />
    </tr>
    <tr>
      <th>context.groupId</th>
      <td id="groupidfield" />
    </tr>
  </table>
</div>
