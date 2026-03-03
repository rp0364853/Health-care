function downloadPDF() {

  let bookings = JSON.parse(localStorage.getItem("appointments")) || [];

  if(bookings.length === 0){
    alert("No bookings to download");
    return;
  }

  let content = `
    <html>
    <head>
      <title>Appointments</title>
      <style>
        body{font-family:Arial;padding:20px;}
        h2{text-align:center;}
        .card{
          border:1px solid #000;
          padding:10px;
          margin-bottom:10px;
        }
      </style>
    </head>
    <body>
      <h2>All Appointment Records</h2>
  `;

  bookings.forEach(b=>{
    content += `
      <div class="card">
        <p><b>Name:</b> ${b.name}</p>
        <p><b>Age:</b> ${b.age}</p>
        <p><b>Doctor:</b> ${b.doctor}</p>
        <p><b>Date:</b> ${b.date}</p>
        <p><b>Time:</b> ${b.time}</p>
      </div>
    `;
  });

  content += `</body></html>`;

  const printWindow = window.open('', '', 'height=600,width=800');
  printWindow.document.write(content);
  printWindow.document.close();
  printWindow.print();
}
