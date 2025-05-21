## WebTop

A web-based Linux (Debian 12 + Xfce) desktop environment.

## Usage

1. Install Docker for your platform
      - Windows: https://docs.docker.com/desktop/setup/install/windows-install/
      - Mac: https://docs.docker.com/desktop/setup/install/mac-install/  
      - Linux-based: https://docs.docker.com/engine/install/

2. Run `docker compose up` in this folder. Use your operating system's terminal application. 

3. Open your browser and go to the site `localhost:3000`. You should be able to see what looks like a user interface (desktop) that looks something like this.

![desktop](images/desktop.png)

4. Your files can be shared / saved in the `data/` folder: this is shared between your OS and the web VM. Try adding a file to `data/Desktop/` and see what happens in the web interface!