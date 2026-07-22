import { getStore } from "@netlify/blobs";

const KEY = "plant-status-tracker-data";

export default async (req) => {
  const store = getStore({ name: "plant-tracker", consistency: "strong" });

  if (req.method === "GET") {
    const value = await store.get(KEY);
    return new Response(JSON.stringify({ value: value ?? null }), {
      headers: { "content-type": "application/json" }
    });
  }

  if (req.method === "POST") {
    const body = await req.json();
    if (typeof body.value !== "string") {
      return new Response(JSON.stringify({ error: "value must be a string" }), {
        status: 400,
        headers: { "content-type": "application/json" }
      });
    }
    await store.set(KEY, body.value);
    return new Response(JSON.stringify({ ok: true }), {
      headers: { "content-type": "application/json" }
    });
  }

  return new Response("Method Not Allowed", { status: 405 });
};

export const config = { path: "/api/plant-data" };
