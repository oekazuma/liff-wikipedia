<script>
  import liff from "@line/liff";

  liff.init({ liffId: LIFF_ID });
</script>

<h1>LIFF Data</h1>
<table border="1">
  <tr>
    <th>language</th>
    <td>{liff.getLanguage()}</td>
  </tr>
  <tr>
    <th>version</th>
    <td>{liff.getVersion()}</td>
  </tr>
  <tr>
    <th>isInClient</th>
    <td>{liff.isInClient()}</td>
  </tr>
  <tr>
    <th>isLoggedIn</th>
    <td>{liff.isLoggedIn()}</td>
  </tr>
  <tr>
    <th>OS</th>
    <td>{liff.getOS()}</td>
  </tr>
  <tr>
    <th>LineVersion</th>
    <td>{liff.getLineVersion()}</td>
  </tr>
</table>
