---
layout: page
title: System Design
category: ref
date: 2016-02-14 19:19:00
---

### <i class="fa fa-chevron-circle-right"></i> High Level Overview
- <a href="/uploads/Architecture_Overview.pdf" target="_blank">Architecture Overview</a>
- <a href="/uploads/Web_Services_Overview.pdf" target="_blank">WebAPI Overview</a>
- <a href="/uploads/HUB_Overview.pdf" target="_blank">HUB Overview</a>
- **Technology Stack**: <a href="https://en.wikipedia.org/wiki/ESP8266" target="_blank">ESP8266</a>, <a href="https://www.lua.org/" target="_blank">Lua</a>, <a href="https://www.python.org/" target="_blank">Python</a>/<a href="http://flask.pocoo.org/" target="_blank">Flask</a>, <a href="https://www.raspberrypi.org/products/raspberry-pi-3-model-b/" target="_blank">Raspberry Pi 3 Model B</a>, <a href="https://www.ruby-lang.org/en/" target="_blank">Ruby</a>/<a href="http://rubyonrails.org/" target="_blank">Ruby on Rails</a>.

### <i class="fa fa-plug"></i> Control Panel & Hub Integration

#### <span class="label label-info">CONTEXT</span> User uploads print job via control panel

1. The user selects a 3D printer and uploads a model via the control panel.
2. The Web API acknowledges receipt of the model, e.g. `200 OK`.
3. The Web API uploads the model to the HUB that corresponds to the selected printer.
4. The HUB acknowedges receipt of the model, e.g. `200 OK`.
5. The HUB notifies the Web API that a new job was created, e.g. `POST /v1/printers/:id/jobs`.
6. The HUB sends the model to the selected 3D printer for printing if it is not busy, otherwise
the job is queued.

#### <span class="label label-info">CONTEXT</span> HUB detects print job status update
1. The HUB communicates the status update to the Web API, e.g. `PATCH /v1/jobs/:id`.
2. The Web API acknowledges the status update, e.g. `200 OK`.
2. If job status changed to `completed`, then HUB does internal cleanup. At this point the HUB is no longer required track updates or hold any information about the job in question.

#### <span class="label label-info">CONTEXT</span> User adds new HUB via control panel
....
#### <span class="label label-info">CONTEXT</span> HUB detects printer status update
....

#### <span class="label label-info">CONTEXT</span> HUB detects sensor reading change
....
