appdir = join_paths(get_option('datadir'), 'applications')
desktop_utils = find_program('desktop-file-validate', required: false)

if get_option('with-gtk')
  hexchat_appdata = i18n.merge_file(
    input: 'hexchat.appdata.xml.in',
    output: 'hexchat.appdata.xml',
    po_dir: '../../po',
    install: true,
    install_dir: join_paths(get_option('datadir'), 'appdata')
  )

  appstream_util = find_program('appstream-util', required: false)
  if appstream_util.found()
    test('Validate hexchat.appdata.xml', appstream_util,
      args: ['validate', hexchat_appdata]
    )
  endif

  desktop_conf = configuration_data()
  if get_option('with-dbus')
    desktop_conf.set('exec_command', 'hexchat --existing %U')
  else
    desktop_conf.set('exec_command', 'hexchat %U')
  endif

  desktop_file = configure_file(
    input: 'hexchat.desktop.in.in',
    output: 'hexchat.desktop.in',
    configuration: desktop_conf
  )

  hexchat_desktop = i18n.merge_file(
    input: desktop_file,
    output: 'hexchat.desktop',
    po_dir: '../../po',
    type: 'desktop',
    install: true,
    install_dir: appdir
  )

  if desktop_utils.found()
    test('Validate hexchat.desktop', desktop_utils,
      args: [hexchat_desktop]
    )
  endif
endif

if get_option('with-theme-manager')
  htm_desktop = i18n.merge_file(
    input: 'htm.desktop.in',
    output: 'htm.desktop',
    po_dir: '../../po',
    type: 'desktop',
    install: true,
    install_dir: appdir
  )

  if desktop_utils.found()
    test('Validate htm.desktop', desktop_utils,
      args: [htm_desktop]
    )
  endif

  install_data('htm-mime.xml',
    install_dir: join_paths(get_option('datadir'), 'mime/packages')
  )
endif
