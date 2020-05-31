# v2ray ws+tls one click setup

## Steps

Follow steps at link: https://ssr.tools/1317

1. Apply vps server

    - [vultr](https://www.vultr.com/)
    - [linode](https://www.linode.com/)
    - [digitalocean](https://www.digitalocean.com/)
    - [bandwagonhost](https://bandwagonhost.com/)
    - [interserver](https://www.interserver.net/)
    - [google cloud](https://cloud.google.com/)
    - [aws](https://aws.amazon.com/)

2. Apply domain name

    - https://www.namesilo.com

3. Setup **A record** to map domain name to the IP address of vps server

    - https://www.imhunk.com/how-to-add-a-record-in-dns/
    - https://www.zhudc.com/website/2413
    - https://blog.csdn.net/huwei2003/article/details/54580614

4. One click install

    ```
    $ bash <(curl -L -s https://raw.githubusercontent.com/wulabing/V2Ray_ws-tls_bash_onekey/master/install.sh) | tee v2ray_ins.log
    ```

    Or

    ```
    wget -N --no-check-certificate -q -O install.sh "https://raw.githubusercontent.com/wulabing/V2Ray_ws-tls_bash_onekey/master/install.sh" && chmod +x install.sh && bash install.sh
    ```

    Or

    ```
    $ git clone https://github.com/wulabing/V2Ray_ws-tls_bash_onekey v2ray_ws-tls_install
    $ cd v2ray_ws-tls_install
    $ chmod a+x install.sh
    $ sudo ./install.sh
    ```

    Then install bbr improvement

    ```
    $ wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh
    ```

    Or

    ```
    $ git clone https://github.com/teddysun/across
    $ cd across
    $ chmod a+x bbr.sh
    $ sudo ./bbr.sh
    ```

5. Done

## Misc

- v2ray on gcp (Google Cloud Platform) howto:
  - https://www.wmsoho.com/google-cloud-platform-ssr-bbr-tutorial/
  - https://hackersandslackers.com/google-cloud-compute-engine/
  - https://233v2.com/post/16/
  - https://zelikk.blogspot.com/2019/01/gcp-v2ray-firewall.html
  - https://medium.com/@moreless/%E8%B0%B7%E6%AD%8C%E4%BA%91%E4%B8%8A%E5%AE%89%E8%A3%85v2ray%E5%9B%BE%E6%96%87%E6%95%99%E7%A8%8B-da93650d0aa3


## Reference

