{
    "dns": {
        "hosts": {
            "geosite:category-ads-all": "127.0.0.1",
            "geosite:category-ads-ir": "127.0.0.1",
            "domain:googleapis.cn": "googleapis.com"
        },
        "servers": [
            "https://94.140.14.14/dns-query",
            {
                "address": "1.1.1.1",
                "domains": [
                    "geosite:private",
                    "geosite:category-ir",
                    "domain:.ir"
                ],
                "expectIPs": [
                    "geoip:cn"
                ],
                "port": 53
            }
        ]
    },
    "fakedns": [
        {
            "ipPool": "198.18.0.0/15",
            "poolSize": 10000
        }
    ],
    "inbounds": [
        {
            "port": 10808,
            "protocol": "socks",
            "settings": {
                "auth": "noauth",
                "udp": true,
                "userLevel": 8
            },
            "sniffing": {
                "destOverride": [
                    "http",
                    "tls",
                    "fakedns"
                ],
                "enabled": true
            },
            "tag": "socks"
        },
        {
            "port": 10809,
            "protocol": "http",
            "settings": {
                "userLevel": 8
            },
            "tag": "http"
        }
    ],
    "log": {
        "loglevel": "warning"
    },
    "outbounds": [
        {
            "protocol": "vless",
            "settings": {
                "vnext": [
                    {
                        "address": "bpb.newfinisher.workers.dev",
                        "port": 443,
                        "users": [
                            {
                                "encryption": "none",
                                "flow": "",
                                "id": "bee0ee58-67bc-4ac5-b8c8-c66084d4a84a",
                                "level": 8,
                                "security": "auto"
                            }
                        ]
                    }
                ]
            },
            "streamSettings": {
                "network": "ws",
                "security": "tls",
                "tlsSettings": {
                    "allowInsecure": false,
                    "alpn": [
                        "h2",
                        "http/1.1"
                    ],
                    "fingerprint": "chrome",
                    "publicKey": "",
                    "serverName": "bpb.NEWfIniSHeR.WORKERS.DEV",
                    "shortId": "",
                    "show": false,
                    "spiderX": ""
                },
                "wsSettings": {
                    "headers": {
                        "Host": "BpB.NewfINisher.WORKers.deV"
                    },
                    "path": "/IpqdjvS6NOaB9_el?ed=2048"
                },
                "sockopt": {
                    "dialerProxy": "fragment",
                    "tcpKeepAliveIdle": 100,
                    "tcpNoDelay": true
                }
            },
            "tag": "proxy"
        },
        {
            "tag": "fragment",
            "protocol": "freedom",
            "settings": {
                "domainStrategy": "AsIs",
                "fragment": {
                    "packets": "tlshello",
                    "length": "100-200",
                    "interval": "10-20"
                }
            },
            "streamSettings": {
                "sockopt": {
                    "tcpKeepAliveIdle": 100,
                    "TcpNoDelay": true
                }
            }
        },
        {
            "protocol": "freedom",
            "settings": {
                "domainStrategy": "UseIP"
            },
            "tag": "direct"
        },
        {
            "protocol": "blackhole",
            "settings": {
                "response": {
                    "type": "http"
                }
            },
            "tag": "block"
        }
    ],
    "policy": {
        "levels": {
            "8": {
                "connIdle": 300,
                "downlinkOnly": 1,
                "handshake": 4,
                "uplinkOnly": 1
            }
        },
        "system": {
            "statsOutboundUplink": true,
            "statsOutboundDownlink": true
        }
    },
    "routing": {
        "domainStrategy": "IPIfNonMatch",
        "rules": [
            {
                "ip": [
                    "1.1.1.1"
                ],
                "outboundTag": "direct",
                "port": "53",
                "type": "field"
            },
            {
                "domain": [
                    "geosite:private",
                    "geosite:category-ir",
                    "domain:.ir"
                ],
                "outboundTag": "direct",
                "type": "field"
            },
            {
                "ip": [
                    "geoip:private",
                    "geoip:ir"
                ],
                "outboundTag": "direct",
                "type": "field"
            },
            {
                "domain": [
                    "geosite:category-ads-all",
                    "geosite:category-ads-ir"
                ],
                "outboundTag": "block",
                "type": "field"
            }
        ]
    },
    "stats": {}
}
