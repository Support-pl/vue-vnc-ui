# vue-vnc-ui

## usage

Import UI from library.
```js
import UI from 'vue-vnc-ui';
```

Create layout.
```html
<template>
  <div id="noVNC_status"></div>

  <div id="noVNC_control_bar_anchor" class="noVNC_vcenter">

    <div id="noVNC_control_bar">
      <div id="noVNC_control_bar_handle" title="Hide/Show the control bar">
        <div></div>
      </div>

      <div class="noVNC_scroll">

        <div @click="removeCanvases">
          <!-- <router-link class="noVNC_button noVNC_button--goBack" :to="{path: `/cloud-${$route.params.pathMatch}`}" title="Go back">
          <a-icon type="left"></a-icon>
        </router-link> -->
          <a class="noVNC_button noVNC_button--goBack" @click="$router.go(-1)" title="Go back">
            <a-icon type="left"></a-icon>
          </a>
        </div>

        <!-- Drag/Pan the viewport -->
        <input type="image" alt="Drag" src="img/images/drag.svg" id="noVNC_view_drag_button"
          class="noVNC_button noVNC_hidden" title="Move/Drag Viewport">

        <!--noVNC Touch Device only buttons-->
        <div id="noVNC_mobile_buttons">
          <input type="image" alt="Keyboard" src="img/images/keyboard.svg" id="noVNC_keyboard_button"
            class="noVNC_button" title="Show Keyboard">
        </div>

        <!-- Extra manual keys -->
        <input type="image" alt="Extra keys" src="img/images/toggleextrakeys.svg" id="noVNC_toggle_extra_keys_button"
          class="noVNC_button" title="Show Extra Keys">
        <div class="noVNC_vcenter">
          <div id="noVNC_modifiers" class="noVNC_panel">
            <input type="image" alt="Ctrl" src="img/images/ctrl.svg" id="noVNC_toggle_ctrl_button"
              class="noVNC_button" title="Toggle Ctrl">
            <input type="image" alt="Alt" src="img/images/alt.svg" id="noVNC_toggle_alt_button" class="noVNC_button"
              title="Toggle Alt">
            <input type="image" alt="Windows" src="img/images/windows.svg" id="noVNC_toggle_windows_button"
              class="noVNC_button" title="Toggle Windows">
            <input type="image" alt="Tab" src="img/images/tab.svg" id="noVNC_send_tab_button" class="noVNC_button"
              title="Send Tab">
            <input type="image" alt="Esc" src="img/images/esc.svg" id="noVNC_send_esc_button" class="noVNC_button"
              title="Send Escape">
            <input type="image" alt="Ctrl+Alt+Del" src="img/images/ctrlaltdel.svg" id="noVNC_send_ctrl_alt_del_button"
              class="noVNC_button" title="Send Ctrl-Alt-Del">
          </div>
        </div>

        <!-- Shutdown/Reboot -->
        <input type="image" alt="Shutdown/Reboot" src="img/images/power.svg" id="noVNC_power_button"
          class="noVNC_button" title="Shutdown/Reboot...">
        <div class="noVNC_vcenter">
          <div id="noVNC_power" class="noVNC_panel">
            <div class="noVNC_heading">
              <img alt="" src="img/images/power.svg"> Power
            </div>
            <input type="button" id="noVNC_shutdown_button" value="Shutdown">
            <input type="button" id="noVNC_reboot_button" value="Reboot">
            <input type="button" id="noVNC_reset_button" value="Reset">
          </div>
        </div>

        <!-- Clipboard -->
        <input type="image" alt="Clipboard" src="img/images/clipboard.svg" id="noVNC_clipboard_button"
          class="noVNC_button" title="Clipboard">
        <div class="noVNC_vcenter">
          <div id="noVNC_clipboard" class="noVNC_panel">
            <div class="noVNC_heading">
              <img alt="" src="img/images/clipboard.svg"> Clipboard
            </div>
            <textarea id="noVNC_clipboard_text" rows=5></textarea>
            <br>
            <input id="noVNC_clipboard_clear_button" type="button" value="Clear" class="noVNC_submit">
          </div>
        </div>

        <!-- Toggle fullscreen -->
        <input type="image" alt="Fullscreen" src="img/images/fullscreen.svg" id="noVNC_fullscreen_button"
          class="noVNC_button noVNC_hidden" title="Fullscreen">

        <!-- Settings -->
        <input type="image" alt="Settings" src="img/images/settings.svg" id="noVNC_settings_button"
          class="noVNC_button" title="Settings">
        <div class="noVNC_vcenter">
          <div id="noVNC_settings" class="noVNC_panel">
            <ul>
              <li class="noVNC_heading">
                <img alt="" src="img/images/settings.svg"> Settings
              </li>
              <template v-if="instance && !isLoading">
                <li>
                  password:
                </li>
                <li>
                  <password :password="instance.config.password"/>
                </li>
              </template>
              <li>
                <hr>
              </li>
              <li>
                <label><input id="noVNC_setting_shared" type="checkbox"> Shared Mode</label>
              </li>
              <li>
                <label><input id="noVNC_setting_view_only" type="checkbox"> View Only</label>
              </li>
              <li>
                <hr>
              </li>
              <li>
                <label><input id="noVNC_setting_view_clip" type="checkbox"> Clip to Window</label>
              </li>
              <li>
                <label for="noVNC_setting_resize">Scaling Mode:</label>
                <select id="noVNC_setting_resize" name="vncResize">
                  <option value="off">None</option>
                  <option value="scale">Local Scaling</option>
                  <option value="remote">Remote Resizing</option>
                </select>
              </li>
              <li>
                <hr>
              </li>
              <li>
                <div class="noVNC_expander">Advanced</div>
                <div>
                  <ul>
                    <li>
                      <label for="noVNC_setting_quality">Quality:</label>
                      <input id="noVNC_setting_quality" type="range" min="0" max="9" value="6">
                    </li>
                    <li>
                      <label for="noVNC_setting_compression">Compression level:</label>
                      <input id="noVNC_setting_compression" type="range" min="0" max="9" value="2">
                    </li>
                    <!-- <li><hr></li> -->
                    <!-- <li>
                <label for="noVNC_setting_repeaterID">Repeater ID:</label>
                <input id="noVNC_setting_repeaterID" type="text" value="">
              </li> -->
                    <!-- <li>
                <div class="noVNC_expander">WebSocket</div>
                <div><ul>
                  <li>
                    <label><input id="noVNC_setting_encrypt" type="checkbox"> Encrypt</label>
                  </li>
                  <li>
                    <label for="noVNC_setting_host">Host:</label>
                    <input id="noVNC_setting_host">
                  </li>
                  <li>
                    <label for="noVNC_setting_port">Port:</label>
                    <input id="noVNC_setting_port" type="number">
                  </li>
                  <li>
                    <label for="noVNC_setting_path">Path:</label>
                    <input id="noVNC_setting_path" type="text" value="websockify">
                  </li>
                </ul></div>
              </li> -->
                    <li>
                      <hr>
                    </li>
                    <li>
                      <label><input id="noVNC_setting_reconnect" type="checkbox"> Automatic Reconnect</label>
                    </li>
                    <li>
                      <label for="noVNC_setting_reconnect_delay">Reconnect Delay (ms):</label>
                      <input id="noVNC_setting_reconnect_delay" type="number">
                    </li>
                    <li>
                      <hr>
                    </li>
                    <li>
                      <label><input id="noVNC_setting_show_dot" type="checkbox"> Show Dot when No Cursor</label>
                    </li>
                    <!-- <li><hr></li> -->
                    <!-- <li>
                <label>Logging:
                  <select id="noVNC_setting_logging" name="vncLogging">
                  </select>
                </label>
              </li> -->
                  </ul>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>

    <div id="noVNC_control_bar_hint"></div>

  </div> <!-- End of noVNC_control_bar -->

  <!-- Transition Screens -->
  <div id="noVNC_transition">
    <div id="noVNC_transition_text"></div>
    <div>
      <input type="button" id="noVNC_cancel_reconnect_button" value="Cancel" class="noVNC_submit">
    </div>
    <div class="noVNC_spinner"></div>
  </div>

  <div id="noVNC_container">
    <!-- Note that Google Chrome on Android doesn't respect any of these,
        html attributes which attempt to disable text suggestions on the
        on-screen keyboard. Let's hope Chrome implements the ime-mode
        style for example -->
    <textarea id="noVNC_keyboardinput" autocapitalize="off" autocomplete="off" spellcheck="false"
      tabindex="-1"></textarea>
  </div>

  <main>
    <div id="vnc-screen" ref='vncscreen'></div>
  </main>
</template>
```

If necessary, import styles from library.
```js
import styles from 'vue-vnc-ui/app/styles/base.css';

<style module></style>
```

Get a token, name of VM and connection link.
```js
this.token = user.token;
this.desktopName = VM.name ?? 'Unknown';
this.url = 'wss://url';
this.connect();
```

Call connection function.
```js
connect() {
  this.$refs.vncscreen.innerHTML = '';
  UI.connect(this.url, this.token);
  UI.prime();
  if (UI.connected) location.reload();
}
```

Add other functions.
```js
credentialsAreRequired() {
  const password = prompt("Password Required:");

  this.rfb.sendCredentials({ password });
},
updateDesktopName(e) {
  this.desktopName = e.detail.name;
},
removeCanvases() {
  const canvases = document.getElementsByTagName('canvas');

  Array.from(canvases).forEach(el => el.remove());
}
```
