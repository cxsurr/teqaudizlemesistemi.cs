using System;
using System.Collections.Generic;

namespace TeqaudSistemi
{
    class Telebe
    {
        private int Id; private string Ad; private string Kurs; private double Gpa;
        
        public int GetId() { return Id; }
        public string GetAd() { return Ad; }
        public double GetGpa() { return Gpa; }
        
        public void SetId(int id) { Id = id; }
        public void SetAd(string ad) { Ad = ad; }
        public void SetKurs(string kurs) { Kurs = kurs; }
        public void SetGpa(double gpa) { Gpa = gpa; }
        
        public void Melumat() { Console.WriteLine("ID:" + Id + " Ad:" + Ad + " Kurs:" + Kurs + " GPA:" + Gpa); }
    }

    class Teqaud
    {
        private int Id; private string Ad; private double MinGpa; private double AyliqMebleg;
        
        public int GetId() { return Id; }
        public double GetMinGpa() { return MinGpa; }
        public double GetAyliqMebleg() { return AyliqMebleg; }
        
        public void SetId(int id) { Id = id; }
        public void SetAd(string ad) { Ad = ad; }
        public void SetMinGpa(double m) { MinGpa = m; }
        public void SetAyliqMebleg(double m) { AyliqMebleg = m; }
        
        public void Melumat() { Console.WriteLine("ID:" + Id + " Teqaud:" + Ad + " MinGPA:" + MinGpa + " Mebleg:" + AyliqMebleg); }
    }

    class Odenis
    {
        private int Id; private string TelebeAdi; private DateTime Tarix; private double Mebleg; private bool Odenilib;
        
        public int GetId() { return Id; }
        public double GetMebleg() { return Mebleg; }
        public bool GetOdenilib() { return Odenilib; }
        
        public void SetId(int id) { Id = id; }
        public void SetTelebeAdi(string t) { TelebeAdi = t; }
        public void SetTarix(DateTime t) { Tarix = t; }
        public void SetMebleg(double m) { Mebleg = m; }
        public void SetOdenilib(bool o) { Odenilib = o; }
        
        public void Melumat()
        {
            string status = Odenilib ? "Odenilib" : "Gozleyir";
            Console.WriteLine("ID:" + Id + " Telebe:" + TelebeAdi + " Tarix:" + Tarix.ToString("dd.MM.yyyy") + " Mebleg:" + Mebleg + " " + status);
        }
    }

    class SistemBazasi
    {
        private List<Telebe> telebeler = new List<Telebe>();
        private List<Teqaud> teqaudler = new List<Teqaud>();
        private List<Odenis> odenisler = new List<Odenis>();
        private int odenisIdCounter = 1;

        public void TelebeElaveEt(Telebe t) { telebeler.Add(t); Console.WriteLine("Telebe elave edildi!"); }
        public void TeqaudElaveEt(Teqaud t) { teqaudler.Add(t); Console.WriteLine("Teqaud növü elave edildi!"); }
        public void ButunTelebeler() { foreach (var t in telebeler) t.Melumat(); }
        public void ButunTeqaudler() { foreach (var t in teqaudler) t.Melumat(); }

        public void TeqaudTeyinEt(int tId, int teqId)
        {
            Telebe sTel = null; foreach (var t in telebeler) if (t.GetId() == tId) sTel = t;
            Teqaud sTeq = null; foreach (var t in teqaudler) if (t.GetId() == teqId) sTeq = t;

            if (sTel == null || sTeq == null) { Console.WriteLine("Xeta: Tapilmadi!"); return; }
            if (sTel.GetGpa() < sTeq.GetMinGpa()) { Console.WriteLine("Netice: GPA azdir!"); return; }

            for (int i = 0; i < 3; i++)
            {
                Odenis o = new Odenis();
                o.SetId(odenisIdCounter++);
                o.SetTelebeAdi(sTel.GetAd());
                o.SetTarix(DateTime.Now.AddMonths(i));
                o.SetMebleg(sTeq.GetAyliqMebleg());
                o.SetOdenilib(false);
                odenisler.Add(o);
            }
            Console.WriteLine("Ugur: 3 ayliq odenis cedveli yaradildi.");
        }

        // YENİ ƏLAVƏ: Yalnız gözləyən ödənişləri göstərən metod
        public void GozleyenleriGoster()
        {
            Console.WriteLine("--- Gozleyen Odenislerin Siyahisi ---");
            bool tapildi = false;
            foreach (var o in odenisler)
            {
                if (!o.GetOdenilib()) 
                {
                    o.Melumat();
                    tapildi = true;
                }
            }
            if (!tapildi) Console.WriteLine("Gozleyen odenis yoxdur!");
        }

        public void OdenisEt(int id)
        {
            foreach (var o in odenisler)
            {
                if (o.GetId() == id)
                {
                    if (!o.GetOdenilib()) { o.SetOdenilib(true); Console.WriteLine("Odenis edildi!"); }
                    else Console.WriteLine("Artiq edilib!");
                    return;
                }
            }
            Console.WriteLine("ID tapilmadi.");
        }

        public void HesabatGoster()
        {
            double odenilen = 0, qalan = 0;
            Console.WriteLine("\n--- Umumi Hesabat ---");
            foreach (var o in odenisler)
            {
                o.Melumat();
                if (o.GetOdenilib()) odenilen += o.GetMebleg();
                else qalan += o.GetMebleg();
            }
            Console.WriteLine("Cemi Odenilib: " + odenilen + " | Cemi Gozleyir: " + qalan);
        }
    }

    class Program
    {
        static void Main()
        {
            SistemBazasi s = new SistemBazasi();

            while (true)
            {
                Console.WriteLine("\n1.Telebe Yarat 2.Teqaud Yarat 3.Siyahilar 4.Teqaud Teyin Et 5.Odenis Et 6.Hesabat 7.Cixis");
                Console.Write("Secim: ");
                int secim = int.Parse(Console.ReadLine());

                if (secim == 1)
                {
                    Telebe t = new Telebe();
                    Console.Write("ID: "); t.SetId(int.Parse(Console.ReadLine()));
                    Console.Write("Ad: "); t.SetAd(Console.ReadLine());
                    Console.Write("Kurs: "); t.SetKurs(Console.ReadLine());
                    Console.Write("GPA: "); t.SetGpa(double.Parse(Console.ReadLine()));
                    s.TelebeElaveEt(t);
                }
                else if (secim == 2)
                {
                    Teqaud teq = new Teqaud();
                    Console.Write("ID: "); teq.SetId(int.Parse(Console.ReadLine()));
                    Console.Write("Teqaud Adi: "); teq.SetAd(Console.ReadLine());
                    Console.Write("Min GPA: "); teq.SetMinGpa(double.Parse(Console.ReadLine()));
                    Console.Write("Ayliq Mebleg: "); teq.SetAyliqMebleg(double.Parse(Console.ReadLine()));
                    s.TeqaudElaveEt(teq);
                }
                else if (secim == 3)
                {
                    Console.WriteLine("-Telebeler-"); s.ButunTelebeler();
                    Console.WriteLine("-Teqaudler-"); s.ButunTeqaudler();
                }
                else if (secim == 4)
                {
                    Console.Write("Telebe ID: "); int tId = int.Parse(Console.ReadLine());
                    Console.Write("Teqaud ID: "); int teqId = int.Parse(Console.ReadLine());
                    s.TeqaudTeyinEt(tId, teqId);
                }
                else if (secim == 5)
                {
                    // YENİ ƏLAVƏ: Ödəniş etməzdən əvvəl gözləyən ID-ləri göstəririk
                    s.GozleyenleriGoster();
                    Console.Write("Odenmek istediyiniz Odenis ID-ni daxil edin: "); 
                    int odId = int.Parse(Console.ReadLine());
                    s.OdenisEt(odId);
                }
                else if (secim == 6) s.HesabatGoster();
                else if (secim == 7) break;
            }
        }
    }
}
