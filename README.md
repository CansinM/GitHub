# Git ve GitHub Rehberi

## 1. Giriş

### Git Nedir?
Git, yazılım projelerinde kod takibini kolaylaştıran, versiyon kontrol sistemi (VCS) olarak kullanılan açık kaynaklı bir araçtır. Geliştiriciler, kodlarını yönetebilir, farklı versiyonlarını saklayabilir ve ekip ile senkronize çalışabilir. 

Git, Linus Torvalds tarafından geliştirilmiş olup, dağıtık bir sistemdir. Yani, her geliştiricinin kendi bilgisayarında projenin tam bir geçmişi bulunur ve internet bağlantısı olmadan da çalışabilir.

📌 **Avantajları:**
- Değişikliklerin takip edilmesi
- Takım çalışmasını kolaylaştırması
- Branch (dal) yapısı ile paralel geliştirme desteği
- Açık kaynak olması

### Git Kurulumu
Git'i aşağıdaki bağlantılardan işletim sisteminize uygun şekilde indirip kurabilirsiniz:
- **Windows:** [Git for Windows](https://git-scm.com/download/win)
- **Mac:** [Git for Mac](https://git-scm.com/download/mac)
- **Linux:** [Git for Linux](https://git-scm.com/download/linux)

Kurulum tamamlandıktan sonra terminal veya komut satırında aşağıdaki komutları çalıştırarak Git'in kurulduğunu doğrulayabilirsiniz:

```sh
 git --version
```

### Basit Terminal Kullanımı
Git'i kullanırken terminal veya komut satırı ile çalışacağız. Temel komutları öğrenmek için aşağıdaki bağlantıya göz atabilirsiniz:
[Terminal Komutları](https://www.codecademy.com/articles/command-line-commands)

Birkaç temel terminal komutu:
```sh
ls      # Bulunduğunuz dizindeki dosyaları listelemek için
cd      # Dizine girmek için
mkdir   # Yeni bir klasör oluşturmak için
touch   # Dosya oluşturmak için
rm      # Dosya silmek için
```

### Kullanıcı Adı ve Email Tanımlama
Git'i kullanmadan önce, kimlik bilgilerinizi tanımlamanız gerekir. Aşağıdaki komutlar ile kullanıcı adınızı ve e-posta adresinizi ayarlayabilirsiniz:

```sh
git config --global user.name "Adınız Soyadınız"
git config --global user.email "email@example.com"
```

Ayarları doğrulamak için:
```sh
git config --global --list
```

Bu adımlardan sonra Git kullanmaya başlayabiliriz! 🚀

---
## 2. Git Temelleri
### Git Init ve Status
Bir dizini Git deposu olarak başlatmak için aşağıdaki komutu kullanılır:
```sh
git init
```
Bu komut, dizinde gizli bir `.git` klasörü oluşturarak Git'in versiyon kontrolünü başlatır.

Depodaki mevcut durum hakkında bilgi almak için:
```sh
git status
```
Bu komut, takip edilmeyen, değiştirilmiş veya hazırlanmış dosyalar hakkında bilgi verir.

### Commit İşlemi
Bir dosyayı versiyon kontrolüne eklemek için önce "staging area"'ya almanız gerekir:
```sh
git add dosya_adı
```
Tüm dosyaları eklemek için:
```sh
git add .
```
Ardından, yapılan değişiklikleri kaydetmek için bir commit işlemi gerçekleştirilir:
```sh
git commit -m "İlk commit mesajı"
```
Commit mesajı, yapılan değişiklikleri açıklamak için önemlidir.

### Git Log
Yapılan commit'leri görmek için:
```sh
git log
```
Bu komut, commit geçmişini, commit mesajlarını ve hash kodlarını gösterir.

Özet görünüm için:
```sh
git log --oneline
```

### .gitignore Kullanımı
`.gitignore` dosyası, versiyon kontrolüne alınmasını istemediğiniz dosyaları belirlemek için kullanılır. Örneğin:
```
node_modules/
.env
*.log
```
Bu dosyaları Git takip etmeyecek ve depoya eklemeyecektir.

**Not:**
Örnek node.js projeleri üzerinde gösterilmiştir. 
- `node_modules/`: Node.js projelerinde bağımlılıkların bulunduğu klasördür, her makinede değişebilir ve versiyon kontrolüne alınmamalıdır.
- `.env`: Çevresel değişkenleri içeren dosyalardır, API anahtarları gibi hassas bilgileri içerebilir.
- `*.log`: Log dosyaları, hata kayıtları ve sistem çıktıları içerdiğinden genellikle Git’e eklenmez.

---
## 3. Git Branch

### Head Kavramı
Git'te **HEAD**, şu an aktif olan branch’i gösterir. Eğer bir branch değiştirilirse, **HEAD** otomatik olarak yeni branch’i işaret eder. 
```sh
git branch
```
Bu komut, mevcut branch’leri listeler ve aktif olanı gösterir.

Yeni bir branch oluşturmak için:
```sh
git branch feature-branch
```
<img src="https://res.cloudinary.com/snyk/image/upload/v1615821731/wordpress-sync/image1-11.png" alt="Branch" width="500">

Branch'ler arası geçiş yapmak için :
```sh
git checkout main
```
Git’in daha yeni sürümünü kullanıyorsanız, checkout yerine switch komutu da kullanabilirsiniz:
```sh
git switch main
```

### Merge
Farklı branch’leri birleştirmek için kullanılır. Öncelikle, ana branch’e geçiş yapılmalıdır:
```sh
git checkout main
```
Daha sonra, birleştirmek istenen branch şu şekilde eklenir:
```sh
git merge feature-branch
```

### Fast Forward
Eğer branch’te herhangi bir ekstra commit yoksa, Git **fast-forward** olarak adlandırılan basit bir birleştirme yapar.
```sh
git merge --ff feature-branch
```
Bu yöntem, commit geçmişini daha temiz tutar.

### Merge Conflict
İki branch’te aynı satırlarda değişiklik yapıldığında **merge conflict** oluşur. Çatışmaları çözmek için:
1. **Hangi dosyalarda çatışma olduğunu görmek için:**
   ```sh
   git status
   ```
2. **Dosyayı düzenleyip çatışmaları manuel çözmek için:**
   ```sh
   nano dosya.txt
   ```
   **Not:** `nano`, terminal tabanlı bir metin editörüdür. Çatışmaları çözmek için dosyayı açtıktan sonra ilgili satırları düzenleyip kaydetmelisiniz. Alternatif olarak, `vim` veya `code` (VS Code) gibi editörler de kullanılabilir.

   **Varsayılan Editör Seçme:**
   Eğer `nano` dışında başka bir editörü kullanmak isterseniz, şu komutla varsayılan editörü değiştirebilirsiniz:
   ```sh
   git config --global core.editor "vim"
   ```
3. **Çözülen dosyayı ekleyerek commit atmak için:**
   ```sh
   git add dosya.txt
   git commit -m "Merge conflict çözüldü"
   ```

### Stash
Bazı durumlarda, değişiklikleri commit etmeden branch değiştirmek veya uzak depodaki güncellemeleri almak isteyebilirsiniz. `git stash` komutu, geçici olarak değişiklikleri kaydeder ve çalışma alanınızı temizler.

**Temel Kullanım:**
```sh
git stash
```
Bu komut, izlenen dosyalardaki değişiklikleri saklar ve çalışma alanını temizler.

**Saklanan Stash’leri Listeleme:**
```sh
git stash list
```
Bu komut, saklanan değişikliklerin bir listesini gösterir.

**Özel Bir Mesaj ile Stash Kaydetme:**
```sh
git stash push -m "Çalıştığım özellik kodları"
```

**Tüm Stash’leri Temizleme:**
```sh
git stash clear
```
Bu komut, tüm stash’leri siler.

### Pop
Kaydedilen stash’i tekrar geri yüklemek için:
```sh
git stash pop
```
Böylece en son saklanan değişiklikler tekrar projeye uygulanır.

---
## 4. Git Geçmişe Dönme

Git’te commit’lere geri dönmek için **commit hash** kullanılır. Her commit, benzersiz bir **hash kodu** ile temsil edilir.

**Commit Hash Öğrenme:**
```sh
git log
```
Bu komut, commit geçmişini ve her commit’e ait kısa hash kodlarını listeler.

### Checkout
**Belirli Bir Commit’e Gitmek İçin:**
```sh
git checkout commit_hash
```

**Hash Nedir?**
Commit hash, Git’in her commit için ürettiği benzersiz bir kimliktir.

### Reset ve Revert
**Reset**: Commit’i tamamen geri almak için kullanılır.
```sh
git reset --hard commit_hash
```
**Revert**: Yeni bir commit oluşturarak değişiklikleri geri alır.
```sh
git revert commit_hash
```

### Git Diff
Dosyalar arasındaki değişiklikleri görmek için kullanılır:
```sh
git diff
```
Bu komut, değişiklikleri satır bazında gösterir.

### Rebase
Commit geçmişini daha düzenli hale getirmek için kullanılır. Özellikle bir branch’in ana branch ile senkronize edilmesi gerektiğinde tercih edilir.

```sh
git rebase main
```
Bu komut, mevcut branch’i `main` branch’inin en güncel haliyle birleştirir. **Farkı:** `merge` gibi yeni bir merge commit oluşturmaz, tüm commit’leri en güncel branch’in üzerine ekler.

📌 **Rebase vs Merge:**
| Merge | Rebase |
|--------|--------|
| Yeni bir merge commit oluşturur | Commit geçmişini temiz ve sıralı tutar |
| Tüm commit'ler korunur | Commit'lerin sıralaması değişebilir |
| Karmaşıklık oluşturabilir | Daha temiz bir commit geçmişi sağlar |

<img src="https://cms-assets.tutsplus.com/uploads/users/585/posts/23191/preview_image/preview.png" alt="Rebase" width="500">

---
## 5. GitHub

### GitHub Nedir?
GitHub, Git ile yönetilen projelerin saklandığı ve paylaşıldığı bir platformdur. Açık kaynak projelerden özel projelere kadar birçok farklı amaç için kullanılabilir. Geliştiricilerin işbirliği yapmasını, kod incelemesini ve proje yönetimini kolaylaştırır.

📌 **GitHub'ın Avantajları:**
- Projeleri uzak bir sunucuda saklama
- Takım çalışmasını kolaylaştırma
- Açık kaynak topluluğuna katkı sağlama
- Versiyon kontrolü ve kod paylaşımı

### Repo (Depo) Oluşturma
GitHub üzerinde yeni bir repository (depo) oluşturmak için:
1. GitHub'a giriş yapın ve **New Repository** seçeneğine tıklayın.
2. Depoya bir isim verin ve açıklama ekleyin.
3. **Public** veya **Private** olarak belirleyin.
4. Gerekirse `.gitignore` ve `README.md` ekleyin.
5. **Create Repository** butonuna tıklayın.

### Repoları Public ve Private Olarak Oluşturma
- **Public (Herkese Açık):** Projenizi tüm dünyayla paylaşabilirsiniz.
- **Private (Özel):** Yalnızca sizin ve yetkilendirdiğiniz kişilerin erişebileceği projelerdir.

### GitHub’a Push Etme
Yerel bilgisayarınızdaki projeyi GitHub’a göndermek için aşağıdaki adımları takip edebilirsiniz:
```sh
git remote add origin https://github.com/kullaniciadi/repository-adi.git
git branch -M main
git push -u origin main
```
Bu komutlar, yerel repository'yi GitHub'a bağlayarak dosyalarınızı yükler.

### Pull Request (PR)
Pull request, değişiklikleri bir branch'ten ana branch'e veya başka bir branch'e birleştirmek için kullanılan bir taleptir.
1. **Yeni bir branch oluşturun ve değişiklik yapın:**
   Bir branch oluşturmak ve ona geçiş yapmak için aşağıdaki komut kullanılır:
   ```sh
   git checkout -b yeni-branch
   ```
   **Detay:** Bu komut şu işlemleri yapar:
   - Yeni bir `yeni-branch` adlı branch oluşturur.
   - Otomatik olarak bu yeni branch’e geçiş yapar.

2. **Commit yapın ve GitHub’a gönderin:**
   ```sh
   git add .
   git commit -m "Yeni değişiklik"
   git push origin yeni-branch
   ```
3. **GitHub’da `Pull Request` butonuna basarak değişiklikleri gözden geçirin ve gönderin.**

### Fetch ve Pull
**Fetch**, uzak depodaki değişiklikleri yerel depoya indirir ama doğrudan birleştirme yapmaz:
```sh
git fetch origin
```
**Pull**, uzak depodaki değişiklikleri indirir ve mevcut branch ile birleştirir:
```sh
git pull origin main
```
| Komut | Ne Yapar? | Çalışma Alanına Etkisi |
|-------|----------|-----------------|
| `git fetch` | Uzak depodaki değişiklikleri indirir ancak çalışma alanına uygulamaz | Çalışma alanı değişmez |
| `git pull` | Uzak depodaki değişiklikleri indirir ve mevcut branch ile birleştirir | Çalışma alanı değişebilir |

**Özet:**
- `fetch`, değişiklikleri yalnızca indirir, birleştirme yapmaz.
- `pull`, değişiklikleri indirir ve doğrudan mevcut branch’e uygular.

### Clone
GitHub’daki bir projeyi bilgisayarınıza kopyalamak için:
```sh
git clone https://github.com/kullaniciadi/repository-adi.git
```
Bu komut, belirtilen GitHub deposunun tam bir kopyasını oluşturur.

### Fork
Bir projeyi kopyalayarak kendi hesabınıza almak için **Fork** işlemi kullanılır. Bu, açık kaynak projelere katkı sağlamak için idealdir. Fork işlemi GitHub üzerinden yapılır ve proje kendi hesabınıza kopyalanır.

---
## 6. IDE'lerde Git Kullanımı

Git, birçok popüler IDE (Entegre Geliştirme Ortamı) ile entegre olarak kullanılabilir. IDE üzerinden Git işlemleri yapmak, komut satırı kullanmaya kıyasla daha kolay ve görsel bir deneyim sunar.
