# Thanh
#!/system/bin/sh
# Lưu vào /sdcard/script.js
# Chạy: frida -U -n "Free Fire Max" -l /sdcard/script.js
var tenThuVien = "libil2cpp.so";
var coSo = null;

var CauHinh = {
    HeSoNhe: 0.00000000000000001,
    NguongKhoaDau: 0.0000000000000001,
    TyLeDau: 0.12,
    KhoangCachToiDa: 999999999999999999999.0,
    HeSoNapDan: 0.0,
    HeSoGiatSung: 0.0,
    HeSoTanDan: 0.0,
    HeSoTocDoBan: 999999999999999.0,
    HeSoTocDoDiChuyen: 999999999999999.0,
    HeSoSatThuongDau: 999999999999999999999999.0,
    SoDanToiDa: 999999999999,
    HeSoXuyenTuong: 1,
    HeSoNoFog: 0.0,
    HeSoNoGrass: 0.0,
    HeSoThoiGian: 0.0000000000000001,
    HeSoHoiMau: 999999999999999999.0,
    HeSoHoiSinh: 1,
    HeSoKhoaDauCung: 0.0000000000000001,
    HeSoNapDanThang: 0.0,
    HeSoGocNhinKhoa: 0.0,
    HeSoAimMagnet: 999999999999999999.0,
    HeSoCamUng: 0.0000000000000001,
    HeSoXuLy: 0.0000000000000001,
    HeSoMang: 100000.0,
    HeSoOnDinhMang: 999999999999999999.0,
    HeSoGiatLui: 0.0,
    HeSoThoiGianHoi: 0.0000000000000001,
    HeSoXoaMau: 999999999999999999999999.0,
    BatNheTam: true,
    BatKhoaDau: true,
    BatKhongGiat: true,
    BatKhongTanDan: true,
    BatTocDoBanCao: true,
    BatVoHanDan: true,
    BatXuyenTuong: true,
    BatSpeedHack: true,
    BatSatThuongDau: true,
    BatNoFog: true,
    BatNoGrass: true,
    BatTocDoGame: true,
    BatAutoHoiMau: true,
    BatAutoHoiSinh: true,
    BatNapDanThang: true,
    BatGocNhinKhoa: true,
    BatAimMagnet: true,
    BatAutoBan: true,
    BatAutoHeadshot: true,
    BatKhoaTarget: true,
    BatToiUuMang: true,
    BatToiUuCamUng: true,
    BatToiUuXuLy: true,
    BatChongBan: true,
    BatTatTacVuNgan: true,
    BatXoaGiatLui: true,
    BatXoaMau: true
};

var Offset = {
    XoayCamera: 0x15A2B40,
    YawPitch: 0x4A2B1D0,
    NguoiChoi: 0x4A2B1C8,
    DanhSachThucThe: 0x4A2B1C0,
    GiatSung: 0x1D2E4F0,
    TanDan: 0x249B1C0,
    TocDoBan: 0x25A2D0,
    XuyenTuong: 0x227F9A0,
    TocDoDiChuyen: 0x1E3A5B0,
    SatThuong: 0x3E39A0,
    AmThanh: 0x205D7E0,
    CoCay: 0x216E8F0,
    Dan: 0x26B3E0,
    ThoiGian: 0x4A2B1E0,
    HoiMau: 0x2B08C0,
    HoiSinh: 0x2C19D0,
    NapDan: 0x26B3E0,
    GocNhin: 0x4A2B1D0,
    AimMagnet: 0x3D28F0,
    AutoBan: 0x1C5D6E0,
    KhoaTarget: 0x3C17E0,
    AutoHeadshot: 0x405BC0,
    Mang: 0x4A2B220,
    OnDinhMang: 0x4A2B230,
    CamUng: 0x4A2B240,
    XuLy: 0x4A2B250,
    GiatLui: 0x4A2B260,
    XoaMau: 0x4A2B270
};

function choThuVien(ten, goiLai) {
    var kiemTra = setInterval(function () {
        var module = Process.findModuleByName(ten);
        if (module) {
            clearInterval(kiemTra);
            goiLai(module.base);
        }
    }, 100);
}

choThuVien(tenThuVien, function (base) {
    coSo = base;
    if (CauHinh.BatNheTam) hookNheTam();
    if (CauHinh.BatKhoaDau) hookKhoaDau();
    if (CauHinh.BatKhongGiat) hookKhongGiat();
    if (CauHinh.BatKhongTanDan) hookKhongTanDan();
    if (CauHinh.BatTocDoBanCao) hookTocDoBan();
    if (CauHinh.BatVoHanDan) hookVoHanDan();
    if (CauHinh.BatXuyenTuong) hookXuyenTuong();
    if (CauHinh.BatSpeedHack) hookSpeedHack();
    if (CauHinh.BatSatThuongDau) hookSatThuongDau();
    if (CauHinh.BatNoFog) hookNoFog();
    if (CauHinh.BatNoGrass) hookNoGrass();
    if (CauHinh.BatTocDoGame) hookTocDoGame();
    if (CauHinh.BatAutoHoiMau) hookAutoHoiMau();
    if (CauHinh.BatAutoHoiSinh) hookAutoHoiSinh();
    if (CauHinh.BatNapDanThang) hookNapDanThang();
    if (CauHinh.BatGocNhinKhoa) hookGocNhinKhoa();
    if (CauHinh.BatAimMagnet) hookAimMagnet();
    if (CauHinh.BatAutoBan) hookAutoBan();
    if (CauHinh.BatKhoaTarget) hookKhoaTarget();
    if (CauHinh.BatAutoHeadshot) hookAutoHeadshot();
    if (CauHinh.BatToiUuMang) hookToiUuMang();
    if (CauHinh.BatToiUuCamUng) hookToiUuCamUng();
    if (CauHinh.BatToiUuXuLy) hookToiUuXuLy();
    if (CauHinh.BatChongBan) hookChongBan();
    if (CauHinh.BatTatTacVuNgan) hookTatTacVuNgan();
    if (CauHinh.BatXoaGiatLui) hookXoaGiatLui();
    if (CauHinh.BatXoaMau) hookXoaMau();
});

function hookNheTam() {
    try {
        Interceptor.attach(coSo.add(Offset.XoayCamera), {
            onEnter: function (args) {
                var deltaX = args[0].toFloat();
                var deltaY = args[1].toFloat();
                var nguoiChoi = layNguoiChoi();
                if (!nguoiChoi) {
                    args[0] = ptr(deltaX * CauHinh.HeSoNhe);
                    args[1] = ptr(deltaY * CauHinh.HeSoNhe);
                    return;
                }
                var mucTieu = timMucTieuGanNhat(nguoiChoi);
                if (!mucTieu) {
                    args[0] = ptr(deltaX * CauHinh.HeSoNhe);
                    args[1] = ptr(deltaY * CauHinh.HeSoNhe);
                    return;
                }
                var goc = tinhGocDenDau(nguoiChoi, mucTieu);
                var conTroGoc = coSo.add(Offset.YawPitch);
                var yawHienTai = Memory.readFloat(conTroGoc);
                var pitchHienTai = Memory.readFloat(conTroGoc.add(0x4));
                var chenhLechYaw = chuanHoaGoc(goc.yaw - yawHienTai);
                var chenhLechPitch = goc.pitch - pitchHienTai;
                var khoangCachGoc = Math.sqrt(chenhLechYaw * chenhLechYaw + chenhLechPitch * chenhLechPitch);
                if (khoangCachGoc <= CauHinh.NguongKhoaDau) {
                    args[0] = ptr(0.0);
                    args[1] = ptr(0.0);
                    Memory.writeFloat(conTroGoc, goc.yaw);
                    Memory.writeFloat(conTroGoc.add(0x4), goc.pitch);
                } else {
                    args[0] = ptr(deltaX * CauHinh.HeSoNhe);
                    args[1] = ptr(deltaY * CauHinh.HeSoNhe);
                }
            }
        });
    } catch (e) {}
}

function hookKhoaDau() {
    try {
        Interceptor.attach(coSo.add(Offset.YawPitch), {
            onEnter: function (args) {
                var nguoiChoi = layNguoiChoi();
                if (!nguoiChoi) return;
                var mucTieu = timMucTieuGanNhat(nguoiChoi);
                if (!mucTieu) return;
                var goc = tinhGocDenDau(nguoiChoi, mucTieu);
                var conTroGoc = coSo.add(Offset.YawPitch);
                Memory.writeFloat(conTroGoc, goc.yaw);
                Memory.writeFloat(conTroGoc.add(0x4), goc.pitch);
            }
        });
    } catch (e) {}
}

function hookKhongGiat() {
    try {
        Interceptor.attach(coSo.add(Offset.GiatSung), {
            onEnter: function (args) {
                if (args[0] && !args[0].isNull()) Memory.writeFloat(args[0], CauHinh.HeSoGiatSung);
            }
        });
    } catch (e) {}
}

function hookKhongTanDan() {
    try {
        Interceptor.attach(coSo.add(Offset.TanDan), {
            onEnter: function (args) {
                if (args[0] && !args[0].isNull()) Memory.writeFloat(args[0], CauHinh.HeSoTanDan);
            }
        });
    } catch (e) {}
}

function hookTocDoBan() {
    try {
        Interceptor.attach(coSo.add(Offset.TocDoBan), {
            onEnter: function (args) {
                if (args[0] && !args[0].isNull()) {
                    var giaTriCu = Memory.readFloat(args[0]);
                    Memory.writeFloat(args[0], giaTriCu * CauHinh.HeSoTocDoBan);
                }
            }
        });
    } catch (e) {}
}

function hookVoHanDan() {
    try {
        Interceptor.attach(coSo.add(Offset.Dan), {
            onEnter: function (args) {
                if (args[0] && !args[0].isNull()) Memory.writeInt
                
