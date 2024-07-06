# Blockchain Node Kurulumu ve Yönetiminde Yardımcı Komutlar

Bu rehber, bir blockchain node'unun kurulumu ve yönetiminde kullanılabilecek bazı örnek komutları içermektedir. Komutları, projenize uygun olacak şekilde değiştirmeyi unutmayın. Örneğin, "örnekd" ve "ÖRNEK" ifadelerini kendi projenizin ismi ile değiştirebilirsiniz.

## Cüzdan İşlemleri

### 1. Cüzdan Oluşturma
Yeni bir cüzdan oluşturmak için:
```bash
örnekd keys add wallet
```

### 2. Var Olan Cüzdanı Geri Getirme / Import Etme
Önceden oluşturulmuş bir cüzdanı geri getirmek / import etmek için:
```bash
örnekd keys add wallet --recover
```

### 3. Mevcut Cüzdanları Listeleme
Tüm mevcut cüzdanları listelemek için:
```bash
örnekd keys list
```

### 4. Cüzdan Silme
Bir cüzdanı silmek için:
```bash
örnekd keys delete wallet
```

### 5. Cüzdan Bakiyesini Öğrenme
Bir cüzdanın bakiyesini öğrenmek için:
```bash
örnekd query bank balances wallet
```

## Validatör İşlemleri

### 6. Validatör Unjail Komutu (Jailden Kurtulma)
Validatörü jail'den kurtarmak için:
```bash
örnekd tx slashing unjail --from cüzdanadın --chain-id chainismi --gas auto -y
```

### 7. Tüm Validatörlerden Ödülleri Çekme
Başka validatörlere delege ettiyseniz tüm validatörlerden ödülleri çekmek için:
```bash
örnekd tx distribution withdraw-all-rewards --from wallet --chain-id atlantic-2 --gas auto -y
```

### 8. Kendi Validatörünüze Ait Komisyon ve Ödülleri Çekme
Kendi validatörünüzden komisyon ve ödülleri çekmek için:
```bash
örnekd tx distribution withdraw-rewards valoperadresiniz --commission --from wallet --chain-id atlantic-2 --gas auto -y
```

### 9. Validatöre Delege Etme
Bir validatöre delege etmek için:
```bash
örnekd tx staking delegate valoperadresi 10000000usei --from=wallet --chain-id atlantic-2 --gas=auto
```

### 10. Başka Cüzdana Transfer
Başka bir cüzdana transfer yapmak için:
```bash
örnekd tx bank send cüzdanadresi hedefcüzdanadresi 1000000usei --from wallet --chain-id atlantic-2 --gas auto -y
```

### 11. Redelege İşlemi
Redelege işlemi yapmak için:
```bash
örnekd tx staking redelegate valoperaddres hedefvaloperadress 10000000usei --from=cüzdanismi --chain-id atlantic-2 --gas=auto
```

Not: İlk adres, hali hazırda delege olduğunuz adresi, hedef adresler ise delege edeceğiniz adresi temsil eder. Komutları girerken chain-id'leri kontrol etmeyi unutmayın.

### 12. Senkronizasyon Durumunu Öğrenme
Senkronizasyon durumunu öğrenmek için:
```bash
örnekd status 2>&1 | jq .SyncInfo
```

Not: Çıktı "false" ise senkron, bloklar eşleşmiş; "true" ise senkron değil, bloklar eşleşmemiş demektir.

### 13. Node ID Öğrenme
Node ID'nizi öğrenmek için:
```bash
örnekd tendermint show-node-id
```

### 14. Proposallarda Oy Kullanma
Proposallarda oy kullanmak için:
```bash
örnekd tx gov vote 1 yes --from wallet --chain-id atlantic-2 --gas auto -y
```

Not: "vote" kelimesinin yanındaki sayı oylama teklifinin sayısını ifade eder. Kaçıncı oylama olduğunu explorerda proposals kısmında görüp komutu modifiye edebilirsiniz. "yes" yazan kısım ise tercihinize bağlı; "no" yazabilirsiniz.

## Servis Komutları

### 15. Servis Dosyasının Durumuna Bakma
Servis dosyasının durumunu kontrol etmek için:
```bash
sudo systemctl status örnekd
```

### 16. Servis Dosyalarını Yeniden Yükleme
Servis dosyalarını yeniden yüklemek için:
```bash
sudo systemctl daemon-reload
```

### 17. Servis Dosyasını Yeniden Başlatma
Servis dosyasını yeniden başlatmak için:
```bash
sudo systemctl restart örnekd
```

### 18. Servis Dosyasını Durdurma
Servis dosyasını durdurmak için:
```bash
sudo systemctl stop örnekd
```

### 19. Logları İzleme
Logları izlemek için:
```bash
sudo journalctl -u örnekd -f -o cat
```
Not: Bu komutlarda "unable to resolve host" gibi bir hata alırsanız, başında "sudo" olmadan komutları aynı şekilde girebilirsiniz.

### 20. Senkronizasyon Durumu
Senkronizasyon durumunu kontrol etmek için:
```bash
örnekd status 2>&1 | jq .SyncInfo
```

### 21. Validatör Durumu
Validatör durumunu kontrol etmek için:

```bash
örnekd status 2>&1 | jq .ValidatorInfo
```

### 22. Node Durumu
Node durumunu kontrol etmek için:
```bash
örnekd status 2>&1 | jq .NodeInfo
```

### 23. Validatör Bilgisi Düzenleme
Validatör bilgilerini düzenlemek için:
```bash
örnekd tx staking edit-validator \
  --moniker=<node_isminiz> \
  --identity=<keybase_id> \
  --website="<websiteniz>" \
  --details="<validatör_açıklamanız>" \
  --chain-id=<ilgili_chain_id> \
  --from=<cüzdan_adınız>
```

---

Bu rehberde yer alan komutlar, blockchain node'unuzun yönetiminde size yardımcı olacaktır. Komutları uygularken, proje ve ağınıza özgü detayları kontrol etmeyi unutmayın.
