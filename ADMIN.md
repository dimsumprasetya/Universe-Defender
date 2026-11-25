# Moderasi skor (Supabase)

Buka Supabase → project `universe-defender` → SQL Editor.

Sembunyikan skor curang (tidak dihapus, bisa dikembalikan):

    update public.scores set hidden = true where nick = 'NAMA';
    update public.scores set hidden = true where id = 123;
    update public.scores set hidden = true where score > 100000 and created_at > now() - interval '1 day';

Kembalikan: `update public.scores set hidden = false where id = 123;`

Hapus permanen: `delete from public.scores where id = 123;` (atau lewat Table Editor).

Lihat kiriman terbaru beserta device/IP: `select id,nick,score,dungeon,wave,device,ip,created_at,hidden from public.scores order by id desc limit 50;`

Aturan otomatis (trigger `scores_guard`): skor dibatasi menurut gelombang & dungeon, menang hanya jika gelombang ≥ 25, maksimal 5 kiriman/menit per nickname dan per perangkat, 12/menit per IP, 60/jam per perangkat. Papan menampilkan satu skor terbaik per nickname.
