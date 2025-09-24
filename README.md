import React, { useState } from "react";

export default function BookingFormArabic({ onBook }) {
  const [name, setName] = useState("");
  const [phone, setPhone] = useState("");
  const [date, setDate] = useState("");

  const handleSubmit = e => {
    e.preventDefault();
    onBook({ name, phone, date });
    setName(""); setPhone(""); setDate("");
  };

  return (
    <form onSubmit={handleSubmit} style={{
      maxWidth: "400px", margin: "40px auto", padding: "24px", background: "#fff", borderRadius: "10px", boxShadow: "0 2px 8px #eee", direction: "rtl"
    }}>
      <h2 style={{textAlign: "center", color:"#1976d2"}}>حجز موعد في عيادة د. بشير محمد طاهر</h2>
      <label>الاسم الثلاثي:</label>
      <input type="text" value={name} onChange={e => setName(e.target.value)} required style={{width:"100%",marginBottom:"10px"}} />
      <label>رقم الجوال:</label>
      <input type="tel" value={phone} onChange={e => setPhone(e.target.value)} required style={{width:"100%",marginBottom:"10px"}} />
      <label>تاريخ ووقت الموعد:</label>
      <input type="datetime-local" value={date} onChange={e => setDate(e.target.value)} required style={{width:"100%",marginBottom:"10px"}} />
      <button type="submit" style={{width:"100%",background:"#1976d2",color:"#fff",padding:"10px",border:"none",borderRadius:"6px"}}>احجز الآن</button>
    </form>
  );
}
