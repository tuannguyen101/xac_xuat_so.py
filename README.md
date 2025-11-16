import math
import random
from collections import Counter

# Hàm thay thế cho math.comb nếu dùng Python cũ
def comb(n, k):
    if hasattr(math, 'comb'):
        return math.comb(n, k)
    return math.factorial(n) // (math.factorial(k) * math.factorial(n - k))

def tinh_xac_suat_co_ban():
    print("=" * 60)
    print("TÍNH XÁC SUẤT CHỌN 6 BỘ SỐ TỪ 1-55")
    print("=" * 60)
    
    total_combinations = comb(55, 6)
    print(f"Tổng số cách chọn 6 số từ 55 số: {total_combinations:,}")
    print(f"Xác suất trúng 1 bộ số: 1/{total_combinations:,}")
    print(f"Xác suất: {1/total_combinations*100:.8f}%")
    print()

def game_don_gian():
    print("🎯 GAME ĐOÁN SỐ ĐƠN GIẢN")
    print("Tôi đang nghĩ 6 số từ 1-55...")
    
    so_bi_mat = random.sample(range(1, 56), 6)
    so_bi_mat.sort()
    
    lan_doan = 0
    trung_so = []
    
    while lan_doan < 10:
        lan_doan += 1
        print(f"\nLần đoán thứ {lan_doan}")
        
        try:
            nhap_so = input("Nhập 6 số (cách nhau bằng dấu phẩy): ")
            so_doan = [int(x.strip()) for x in nhap_so.split(',')]
            
            if len(so_doan) != 6 or any(x < 1 or x > 55 for x in so_doan):
                print("Vui lòng nhập 6 số từ 1-55!")
                continue
                
            so_trung = set(so_doan) & set(so_bi_mat)
            print(f"Số trùng: {sorted(so_trung)}")
            
            if len(so_trung) == 6:
                print("🎉 CHÚC MỪNG! Bạn đã đoán đúng cả 6 số!")
                break
                
        except ValueError:
            print("Vui lòng nhập số hợp lệ!")
    
    print(f"\nKết quả: {so_bi_mat}")

def tao_bo_so_may_man():
    print("\n" + "=" * 40)
    print("TẠO 6 BỘ SỐ MAY MẮN")
    print("=" * 40)
    
    for i in range(6):
        bo_so = random.sample(range(1, 56), 6)
        bo_so.sort()
        print(f"Bộ số {i+1}: {bo_so}")

# Chương trình chính đơn giản
if __name__ == "__main__":
    while True:
        print("\n" + "=" * 50)
        print("CHƯƠNG TRÌNH XỔ SỐ ĐƠN GIẢN")
        print("=" * 50)
        print("1. Tính xác suất cơ bản")
        print("2. Chơi game đoán số")
        print("3. Tạo 6 bộ số may mắn")
        print("4. Thoát")
        
        choice = input("Chọn chức năng (1-4): ")
        
        if choice == '1':
            tinh_xac_suat_co_ban()
        elif choice == '2':
            game_don_gian()
        elif choice == '3':
            tao_bo_so_may_man()
        elif choice == '4':
            print("Cảm ơn!")
            break
        else:
            print("Vui lòng chọn 1-4")
