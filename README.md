万能视频解析与下载（前端静态页 + FastAPI + yt-dlp）。请仅下载您有权使用的内容。

运行
cd backend
python -m venv ../.venv && source ../.venv/bin/activate  # Windows 用 .venv\Scripts\activate
pip install -r ../requirements.txt
uvicorn main:app --reload --host 127.0.0.1 --port 8000
浏览器打开 http://127.0.0.1:8000/。API 文档：http://127.0.0.1:8000/api/docs。

必须在 backend 目录下启动，否则 uvicorn 找不到 main 或 config 模块。

打不开 http://127.0.0.1:8000/ 时
看终端是否报错：若未出现 Uvicorn running on http://127.0.0.1:8000，说明进程没起来（常见：未 cd backend、未装依赖、Python 路径不对）。
8000 端口被占用或卡住：浏览器一直转圈、curl 能连上但无响应时，多半是旧进程占着端口。在终端执行：
lsof -i :8000
记下 LISTEN 那一行的 PID，再执行 kill <PID>（仍不退出可用 kill -9 <PID>），然后重新 uvicorn。
换端口（不折腾杀进程时）：
uvicorn main:app --reload --host 127.0.0.1 --port 8001
浏览器改为打开 http://127.0.0.1:8001/。
依赖说明
强烈建议安装 ffmpeg：B 站等站点多为「最佳画质 = 视频轨 + 音频轨」，yt-dlp 需 ffmpeg 合并；未安装时本站「一键下载」会提示失败。macOS：brew install ffmpeg。
环境变量见仓库根目录 .env.example。
测试
pip install -r requirements.txt
pytest