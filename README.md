# 250519
import { useState } from 'react';
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Upload } from 'lucide-react';

export default function FestivalInvitePage() {
  const [title, setTitle] = useState("제17회 다문화 어울림 축제");
  const [date, setDate] = useState("2025년 6월 14일 (토)");
  const [location, setLocation] = useState("임실치즈테마파크");
  const [schedule, setSchedule] = useState(`10:00 ~ 10:30 | 개회식\n10:30 ~ 12:00 | 다문화 공연\n12:00 ~ 13:30 | 점심시간 / 자유 체험\n13:30 ~ 15:00 | 체험 및 홍보 부스 참여\n15:00 ~ 16:00 | 경품 추첨 및 폐회식`);
  const [boothInfo, setBoothInfo] = useState(`1번 부스: 한국문화홍보\n2번 부스: 몽골문화체험\n3번 부스: 베트남 전통놀이\n...\n25번 부스: 글로벌 먹거리 체험`);
  const [image, setImage] = useState(null);

  const handleImageUpload = (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onloadend = () => {
        setImage(reader.result);
      };
      reader.readAsDataURL(file);
    }
  };

  return (
    <div className="max-w-xl mx-auto p-4 space-y-6">
      <h1 className="text-3xl font-bold text-center">🎉 축제 초대장 🎉</h1>
      <div className="space-y-2">
        <Input value={title} onChange={(e) => setTitle(e.target.value)} placeholder="행사 제목" />
        <Input value={date} onChange={(e) => setDate(e.target.value)} placeholder="날짜" />
        <Input value={location} onChange={(e) => setLocation(e.target.value)} placeholder="장소" />
      </div>
      <div>
        <label className="block font-semibold mb-1">행사 스케줄</label>
        <Textarea value={schedule} onChange={(e) => setSchedule(e.target.value)} rows={6} />
      </div>
      <div>
        <label className="block font-semibold mb-1">부스 소개 (번호 + 이름)</label>
        <Textarea value={boothInfo} onChange={(e) => setBoothInfo(e.target.value)} rows={6} />
      </div>
      <div>
        <label className="block font-semibold mb-1">행사 이미지 업로드</label>
        <input type="file" accept="image/*" onChange={handleImageUpload} className="hidden" id="file-upload" />
        <label htmlFor="file-upload" className="cursor-pointer inline-flex items-center px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700">
          <Upload className="mr-2 h-4 w-4" /> 이미지 선택
        </label>
        {image && <img src={image} alt="행사 이미지" className="mt-4 rounded-lg shadow-md" />}
      </div>

      <Card className="mt-6">
        <CardContent className="p-4 space-y-2">
          <h2 className="text-xl font-semibold">{title}</h2>
          <p className="text-gray-600">📅 {date}</p>
          <p className="text-gray-600">📍 {location}</p>
          <div>
            <h3 className="font-bold mt-2">⏰ 행사 스케줄</h3>
            <pre className="whitespace-pre-wrap text-sm text-gray-800">{schedule}</pre>
          </div>
          <div>
            <h3 className="font-bold mt-2">🎪 부스 안내</h3>
            <pre className="whitespace-pre-wrap text-sm text-gray-800">{boothInfo}</pre>
          </div>
          {image && (
            <div>
              <h3 className="font-bold mt-2">🗺️ 부스 위치도</h3>
              <img src={image} alt="부스 위치도" className="mt-2 rounded-lg shadow" />
            </div>
          )}
        </CardContent>
      </Card>
    </div>
  );
}
